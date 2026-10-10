With Linux, you have access to the complete set of libraries and programming utilities and the complete kernel and library source code.

Within the Unix software world, systems and applications are often programmed in C or C++. The standard C and C++ compiler for Linux is GNU GCC, which is an advanced, modern compiler that supports C++, including ATT 3.0 features, as well as Objective-C, another object-oriented dialect of C.

Besides C and C++, other compiled and interpreted programming languages have been ported to Linux, like Smalltalk, FORTRAN, Java, Pascal, LISP, Scheme, and Ada (if you’re masochistic enough to program in Ada, we aren’t going to stop you). In addition, various assemblers for writing protected-mode 80386 code are available, as are Unix hacking favorites like Perl (the script language used to call all script languages) and Tcl/Tk (a shell-like command-processing system that has support for developing simple X Window System applications).

The advanced gdb debugger can step through a program one line of source code at a time or examine a core dump to find the cause of a crash. The gprof profiling utility provides performance statistics for your program, telling you where your program spends most of its execution time. As mentioned above, the emacs text editor provides interactive editing and compilation environments for various programming languages. Other tools include GNU make and imake, which manage compilation of large applications, and RCS, a system for source code locking and revision control.

Finally, Linux supports dynamically linked, shared libraries (DLLs), which result in much smaller binaries. The common subroutine code is linked at runtime. These DLLs let you override function definitions with your own code. For example, if you wish to write your own version of the malloc() library routine, the linker will use your new routine instead of the one in the libraries.

# Introduction to the X Window System

The X Window System, or simply X, is a standard graphical user interface (GUI) for Unix machines and is a powerful environment that supports many applications. Using the X Window System, you can have multiple terminal windows on the screen at once, each having a different login session. A pointing device like a mouse is often used with X, although it isn’t required.