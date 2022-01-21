Known-plaintext attack
==========================

Keynote
---------

	- Cracking ZIP files
	- You need to have one of the original files that compress in the encrypted archive


Tools
-------

	- pkcrack
	- binarywalk
	- dd ( Linux command )
	- strings

My observation
----------------

.. image:: Images/meow.png

看起來就是一張很可愛的Pusheen圖片,沒什麼頭緒,用file 看也很正常是張圖片。

用strings 看一下
::

	meow/UT
	[Wux
	meow/flagUT
	[Wux
	meow/t39.1997-6/UT
	[Wux
	meow/t39.1997-6/p296x100/UT
	[Wux
	meow/t39.1997-6/p296x100/10173502_279586372215628_1950740854_n.pngUT

疑，目錄結構（? 看起來這圖片檔裏面應該藏了一個壓縮檔

binwalk 看一下
::


	DECIMAL       HEXADECIMAL     DESCRIPTION
	--------------------------------------------------------------------------------
	0             0x0             PNG image, 296 x 279, 8-bit/color RGBA, non-interlaced
	41            0x29            Zlib compressed data, compressed
	48543         0xBD9F          Zip archive data, at least v1.0 to extract, name: meow/
	48606         0xBDDE          Zip archive data, encrypted at least v2.0 to extract, compressed size: 51, uncompressed size: 47, name: meow/flag
	48740         0xBE64          Zip archive data, at least v1.0 to extract, name: meow/t39.1997-6/
	48814         0xBEAE          Zip archive data, at least v1.0 to extract, name: meow/t39.1997-6/p296x100/
	48897         0xBF01          Zip archive data, encrypted at least v2.0 to extract, compressed size: 48404, uncompressed size: 48543, name: meow/t39.1997-6/p296x100/10173502_279586372215628_1950740854_n.png
	97912         0x17E78         End of Zip archive, footer length: 22


哦，ZIP耶

unzip一下
::

	> unzip -l meow.png
	Archive:  meow.png
	warning [meow.png]:  48543 extra bytes at beginning or within zipfile
	  (attempting to process anyway)
	  Length      Date    Time    Name
	---------  ---------- -----   ----
	        0  2016-06-11 16:22   meow/
	       47  2016-06-11 16:22   meow/flag
	        0  2016-06-11 16:20   meow/t39.1997-6/
	        0  2016-06-11 16:21   meow/t39.1997-6/p296x100/
	    48543  2014-05-14 05:59   meow/t39.1997-6/p296x100/10173502_279586372215628_1950740854_n.png
			---------                     -------
			    48590                     5 files


Bingo~百分百在圖片後面藏的是ZIP檔啦，連ZIP前面有多少bytes是圖片data都告訴你了XD

而且看到meow/t39.1997-6/p296x100/10173502_279586372215628_1950740854_n.png 這張圖片的大小竟然也是48543，擺明的就是要我們用Known-plaintext attack

所以我們要先取得原檔，試著將圖片分離出來
::

	dd if=meow.png of=mymeow.png bs=48543 count=1

取得原圖片檔之後，將圖片壓縮
::

	zip plaintext.zip mymeow.png

用binwalk把藏在裏面的zip檔拉出來
::

		binwalk -e meow.png

之後就可以看到裏面有個zip檔啦，算一下bytes大小，原圖就是這個拉出來的zip + mymeow.png

最後使用pkcrack
::

	pkcrack -C BD9F.zip -c "meow/t39.1997-6/p296x100/10173502_279586372215628_1950740854_n.png" -P plaintext.zip -p "mymeow.png" -d decrypted.zip -a

成功拿到flag~

Reference
----------

[1] : Binary walk  https://github.com/devttys0/binwalk/wiki/Quick-Start-Guide

[2] : pkcrack https://www.hackthis.co.uk/articles/known-plaintext-attack-cracking-zip-files

[3] : AIS3 2015 writeup :  http://joyhuang9473.github.io/post-ctf/2015/07/27/ais3-writeup-misc2.html
