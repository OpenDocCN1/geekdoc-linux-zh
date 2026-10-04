# D.8 Tuba

# D.7.1 Compiling tcl-debug under Unix

The tcl-debug package is distributed as a gzipped tar archive with a configure file.

To compile tcl-debug on a Unix/Linux system:

+   1. Mount the Tcl/Tk for Real Programmers CD-ROM.

+   2. Change directory to the top of your source tree.
cd /home/example/src

+   3. Unpack the tcl-debug source distribution.
gunzip -c /cdrom/devel/tcl_debug/tcldebug.tgz | tar -xvf

+   4. Change to the tcl-debug directory.
cd tcl-debug-1.7

+   5. Create the Makefile by running the configure script.
configure

+   6. Make the tcl-debug executable.
make

# D.8 Tuba

The Tuba debugger is a Tcl language package that is supported on Unix/ Linux and MS-Windows platforms. This revision does not work on Macintosh.

# D.8.1 Installing the Tuba Debugger under MS-Windows

The MS-Windows distribution of the Tuba debugger is contained in the file devel\tuba23.zip. This can be extracted using the common pkunzip, Gnu unzip or winzip utilities.