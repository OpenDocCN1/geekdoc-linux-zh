# Appendix D. Installing Tcl/Tk Packages

+   3. Unpack the tclcheck source distribution.
gunzip -c /cdrom/devel/tclcheck/tclcheck.tgz | tar -xvf -
4. Change to the tclcheck directory.
cd tclcheck-1.1.12
5. Create the Makefile by running the configure script.
configure
6. Make the tclcheck executable.
make

# D.6 tclparse

The tclparse distribution is on the CD-ROM in the file devel/tclparse/parse300.tgz. This package does not compile with VC++.
To compile this package on a Unix system:

+   1. Mount the Tcl/Tk for Real Programmers CD-ROM.
2. Change directory to the top of your source tree.
cd /home/example/src
3. Unpack the tclparse source distribution.
gunzip -c /cdrom/devel/tclparse/parse300.tgz | tar -xvf -
4. Change to the tclparse directory.
cd tclparse-3.00
5. Make the tclparse executable.
make

# D.7 tcl-debug

The tcl-debug distribution is on the CD-ROM in the file devel tcl-debug/tcldebug.tgz.