2016/12/24 - How to compile iSpy source code via VS2015 on my PC
=================================================================

Preparation
------------

1. Windows OS (I run it on Windows 10 64bits)
2. Download iSpy `source code  <https://github.com/ispysoftware/iSpy>`_ on Github
3. Vistual Studio 2015
4. For building the Setup project `[Wix Toolset 3.10+] <http://wixtoolset.org/>`_ must be installed. (Make sure you restart Visual Studio after installing)

Guide (64 bits)
------------------
0. Don't open and compile the file before doing these steps below.
1. Move the *Video.FFMPEG.64.vcxproj* and *Video.FFMPEG.vcxproj* away from */iSpy-master/FFMPEG*. Don't delete them, just keep them in another directory.
2. Copy all files under the path */iSpy-master/FFMPEG/ffmpeg64/bin* and paste to */iSpy-master/FFMPEG/bin* .
3. Copy the dll: */iSpy-master/FFMPEG/ffmpeg64/bin/iSpy.Video.FFMPEG.dll * and paste to */iSpy-master/FFMPEG/bin*. (If *iSpy.Video.FFMPEG.dll* is already existed in */iSpy-master/FFMPEG/bin* , just delete or replace it. )
4. Open .sln file */iSpy-master/iSpy64.sln* (you may see the error message box like the picture1 below, just click "OK"). Press **F5** to build and run the project , it would be failed and show error message like the picture 2 below. That's all right!

Picture 1:

  .. image:: Images/error01.png

Picture 2 :

  .. image:: Images/error02.png

5. Now move back *Video.FFMPEG.64.vcxproj* and *Video.FFMPEG.vcxproj* back to */iSpy-master/FFMPEG* which moved away in step 1.

6. Press **F5** to run again, and iSpy finally shows up!

Why we need these wired steps?
------------------------------

According to the `readme <https://github.com/ispysoftware/iSpy/blob/master/readme.txt>`_ ,
the FFMPEG project requires that visual studio 2010 is installed. FFMPEG project on visual studio 2015 is considered to an error because of "Not Safety". So we have to do the steps above and do not load this project in our solution explore( in solution, we can unload *iSpy.Video.FFMPEG* project ).

.. image:: Images/load_failed.png
