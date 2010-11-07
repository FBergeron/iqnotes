I tried to port the iqnotes application to qt-4.  I have a branch for this.  But it requires too much work, I think.

I also tried to compile the latest version of Q... using cygwin so that I can just compile the iqnotes's code as is using Qt-3 but it didn't work. 

I'm now trying to use an old binary of Qt-3 (qt-win-free-mingw-3.3.4 to be more precise) to compile the iqnotes application.  It gives some errors for now.  I have a branch for that too.

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
