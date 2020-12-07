What is JZMQ?
-------------

This is the Java language binding for libzmq (aka ZeroMQ, 0MQ).

[![Build Status](https://travis-ci.org/zeromq/jzmq.png?branch=master)](https://travis-ci.org/zeromq/jzmq)

The latest [javadocs](http://zeromq.github.com/jzmq/javadocs/).

Before Starting
---------------
Make sure you download + Install the [Java Runtime](https://www.oracle.com/java/technologies/javase-jre8-downloads.html) and [Development kit](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html). You may need to sign up for an Oracle account.

After downloading the Java Runtime and Development kit, make sure you have a version of [Visual Studio](https://visualstudio.microsoft.com/) and [CMAKE GUI](https://cmake.org/download/) but you can choose to use the command prompt if you would like.

Building and Installing Libzmq
------------------------------
Clone the source code from [here](https://github.com/zeromq/libzmq) or download any release and unpack to any folder. I will refer to this folder as "libzmq" from now on.

After cloning, open up CMAKE and chose the folder where the source code is ("libzmq") and choose a folder to output the configuration (I will refer to this folder as "libzmq-out"). After configuring your folders, press configure and it might come up with a dialog box where it says to choose your compiler. Make sure to choose the correct version of Visual Studio. 

See this image if you're confused:
![CMAKE Configuration](https://github.com/appliedengineering/jzmq/blob/master/Documentation/Images/libzmq.jpg?raw=true)

After pressing configure, you should be presented with a bunch of options highlighted in red. ***MAKE SURE TO CHECK with-drafts option*** 

Then, press generate. This should generate a VS project. Open the project and build it by first changing Debug to Release next to the the Local Windows Debugger then going to the top bar of the window and going Build->Build Solution.

Now, you should have your .libs in lib/release/

Take both libzmq-(v...).lib files and rename the shorter name to libzmq.lib. In my case, it was renaming libzmq-v142-mt-4_3_4.lib to libzmq.lib. Copy this file to another folder which I will refer to as "zmq"

Next, you will need two .h files which can be found [here](https://github.com/zeromq/libzmq/tree/master/include)

Copy all of these files to the "zmq" folder.

Building Windows 64bit with CMake & NMake
-----------------------------------------


1. create a new and empty directory:
```
d:\temp\>mkdir JZMQ
d:\temp\>cd JZMQ
d:\temp\JZMQ\>
```
2. Clone the repository to your new directory
```
d:\temp\JZMQ\>git clone https://github.com/zeromq/jzmq.git
```
3. dive into the checkedout repository and create a new build64 folder
```
d:\temp\JZMQ\>cd jzmq\jzmq-jni
d:\temp\JZMQ\jzmq\jzmq-jni\>mkdir build64
d:\temp\JZMQ\jzmq\jzmq-jni\>cd build64
```
4. Now call CMake to generate the project

You can do this by opening CMAKE Gui and choosing JZMQ\jzmq\jzmq-jni folder as your source code.
Then, choose JZMQ\jzmq\jzmq-jni\build64 as your output.

Click configure like how we did with the libzmq steps above.

Afterwards, you will be presented with a couple of options. For ZMQ_C_INCLUDE_PATH and ZMQ_C_LIB_PATH options, choose the "zmq" folder that we created above. It should still contain the two .h files and the one "libzmq.lib" file.

Next, click generate to create the VS project.

Open the VS project.

In the project jzmq, you will find the CMakeLists.txt. You will have to open it and replace all $$ in the file with $.

After doing that, build the project by Build->Build Solution just like above.

It should complete without any errors and the zmq.jar and jzmq.lib, jzmq.dll files can be found at \JZMQ\jzmq\jzmq-jni\build64\lib


Avoiding JNI
------------

JZMQ uses JNI to wrap libzmq for the best performance. If performance isn't your primary goal, look at the [JeroMQ](https://github.com/zeromq/jeromq) project, which is a pure Java implementation that provides an identical API to JZMQ, and uses the same protocol.

Building Packages
-----------------

To build a Debian package, run:

```bash
$ dpkg-buildpackage -rfakeroot
```

To build an RPM package, run:

```bash
$ rpmbuild -tb jzmq-X.Y.Z.tar.gz
```

Where X.Y.Z is replaced with the version that you've downloaded.

If configure can't find your libzmq installation, you can tell it where to look, using e.g. `--with-zeromq=/usr/local`.

You may want to take a look at http://www.zeromq.org/docs:tuning-zeromq for additional hints.

For more information, refer to the ØMQ website at http://www.zeromq.org/.

On Mac OS X you may need to compile and make install pkg-config if configure fails with "syntax error near unexpected token newline".   
See http://stackoverflow.com/questions/3522248/how-do-i-compile-jzmq-for-zeromq-on-osx for details.   

You may also need to symlink the header files of your standard Java installation (e.g. `/Developer/SDKs/MacOSX10.6.sdk/System/Library/Frameworks/JavaVM.framework/Versions/CurrentJDK/Headers/*.h`) into a suitable directory (e.g. `/usr/local/include`) and point the `JAVA_HOME` environment variable to the parent directory (e.g.`/usr/local`).

## Acknowledgements

YourKit is kindly supporting ZeroMQ project with its full-featured [Java Profiler](http://www.yourkit.com/java/profiler/index.jsp).

Copying
-------

Free use of this software is granted under the terms of the GNU Lesser General
Public License (LGPL). For details see the files `COPYING` and `COPYING.LESSER`
included with the Java binding for ØMQ.
