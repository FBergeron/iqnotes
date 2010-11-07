This is a fork of the old iqnotes application that was (is?) available on the Zaurus.  Someone asked me to build the application on Windows so here is what I did after retrieving the original source code.

First, I tried to port the iqnotes application to qt-4.  But I realized quickly that it would require too much work.

Then, I tried to compile the latest version of Q... using cygwin so that I can just compile the iqnotes's code, as is, using Qt-3.  Unfortunately, it didn't work.

Finally, I have used an old binary of Qt-3 (qt-win-free-mingw-3.3.4 to be more precise that I have found on the SourceForge's qtwin project (http://sourceforge.net/projects/qtwin/) and it worked.

What to do to build the application:

Rename my cygwin directory from n:\cygwin to n:\cygwin.old.  This is needed because my cygwin installation interfers with mingw.

Run setenv.bat that basically does this:

SET QTDIR=N:\Qt\qt-win-free-mingw-3.3.4
SET PATH=%QTDIR%\bin;%PATH%
set QMAKESPEC=win32-g++

After that, I edit the iqnotes.pro file and change these 4 lines:

desktop:DEFINES = IQNOTES_PICDIR="\"pics\""
desktop:INTERFACES = p:\fred\iqnotes-2.1.0rc1\iqnotes\desktop\ui\*.ui
desktop:HEADERS += p:\fred\iqnotes-2.1.0rc1\iqnotes\desktop\qpe\*.h
desktop:SOURCES += p:\fred\iqnotes-2.1.0rc1\iqnotes\desktop\qpe\*.cpp

Then, I do:

cd iqnotes
qmake

Then, I edit the Makefile and replace "-lqt" by "lqt-mt".  mt stands for MultiThread.  It's the only version available in qt-win-free-mingw-3.3.4.

I build the application doing:

make

For some mysterious reasons, the linking step may give some errors.  If I do "make clean;make", it usually works on the second time.  Go figure...

At this point, I should have a iqnotes.exe in the parent directory.  

I package the application manually in a directory that contains:
- iqnotes.exe
- qt-mt3.dll (taken from qt-win-free-mingw-3.3.4 directory)
- mingwm10.dll (taken from qt-win-free-mingw-3.3.4 directory)
- pics folder (taken from iqnotes)

That's it!  I hope I have not forgotten anything.
