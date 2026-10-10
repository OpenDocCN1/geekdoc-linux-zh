install destination is not in your target file system, then you need to copy the libraries to the target file system. Add an environment variable, QTLIB, to the BBB that points to the QT libraries.

If your display cape has a touchscreen, you will probably also want to get and build tslib, the touchscreen library. Get tslib from github with this command executed in your home directory:

```
git clone https://github.com/kergho/tslib.git tslib
```

cd to the newly created `tslib/` and execute the following:

```
export CROSS_COMPILE=arm-unknown-linux-gnueabi-
export CC=arm-unknown-linux-gnueabi-gcc
export CXX=arm-unknown-linux-gnueabi-g++
./autogen.sh
./configure --host=arm-linux-gnueabi --prefix=~/tslib/tslib
make
make install
```

There is an error in the make step. If you have gotten this far in the book, you have probably already googled a few error messages. And if you have not, here is a good time to try it. The solution is relatively obscure, but pretty simple to implement. After `make install` completes, copy the `tslib/bin` and `tslib/lib` directories to `/usr` in your target file system. Copy `tslib/etc/ts.conf` to `/etc` in the target file system.

# Create Build Environment for Target Applications

To build QT applications for the BBB, you must use the tools in the version of QT that we built for the ARM. Change your PATH variable to point to where you installed QT, rather than `/usr/lib64/qt4/bin`. I used the default location, `/usr/local/Trolltech/QtEmbedded-4.8.5-arm/bin`.

There are three variables that need to be added to the project file:

```
QMAKE_CC=arm-unknown-linux-gnueabi-gcc
QMAKE_CXX=arm-unknown-linux-gnueabi-g++
QMAKE_LINK=arm-unknown-linux-gnueabi-g++
```

Remember to add these variables each time you create a project file. There should be a way to do this automatically through qmake’s configuration, but I have not figured it out yet.

Even though you are now using tools from the ARM version of QT, Qt Designer is still the one that came with the CentOS version.