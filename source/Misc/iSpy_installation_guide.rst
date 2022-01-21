2016/12/04 - iSpy installation guide
====================================

Install
--------
Note : You have to use iSpy on **Windows** operation system.

  1. Go to download iSpy on this `page <http://www.ispyconnect.com/download.aspx>`_ .
  2. Install and start the software.
  3. Done.

How to add IP Camera in iSpy
-----------------------------

Open iSpy software -> Add -> IP Camera -> Choose video sorce:

  1.D-Link DCS910(in Lab 409) has to use *MJPEG URL* , username = admin and no password, URL = http://10.21.20.178/video.cgi

  2.HLC-74ED(in Room 108) has to use *FFMPEG(H264)* and URL = rtsp://10.21.6.40 or http://admin:409409@10.21.6.40/GetStream.cgi?Video=0

The result may like this :

.. image:: Images/iSpy.png

How to access iSpy via Website
-------------------------------

Go to this `webpage <https://www.ispyconnect.com/monitor/login.aspx#/page/login>`_ and login by lab409/lab802.16 .

Then choose *Video Wall* to watch video in real time.(But only on the computer that you execute  iSpy. )

**Note : If we want to use this Remote Access implementation, we have to subscribe and pay money...**
