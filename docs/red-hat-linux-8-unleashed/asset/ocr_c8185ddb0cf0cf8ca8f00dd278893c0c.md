Using the C Programming Project Management Tools Provided with Red Hat Linux 699

# Using the C Programming Project Management Tools Provided with Red Hat Linux

Red Hat Linux is replete with tools that make your life as a C/C++ programmer easier. There are tools to create programs (editors), compile programs (gcc and g++), create libraries (ar), control the source (Revision Control System [RCS]) and the Concurrent Versions System [CVS], build code (make), debug programs (gdb and ddd), and determine where inefficiencies lie (gprof).

The following sections introduce some of the programming and project management tools included with Red Hat Linux. This book's CD-ROMs contain many of these tools, which you can use to help software development projects. If you have some previous UNIX experience, you will be familiar with most of these programs because they are traditional complements to a programmer's suite of software.

# Building Programs with make

You use the make command to automatically build and install a C program. The make command's roots stem from an early version of System V UNIX. The version of make that is included with Red Hat Linux is part of the GNU utilities distribution.

# Using Makefiles

The make command automatically builds and updates applications by using amakefile. Makefile is a text file that can contain instructions about which options to pass on to the compiler preprocesser, the compiler, the assembler, and the linker. The make also specifies other things, which source files need to be compiled (and the compiler command line) for a particular code module and which code modules are needed to build the program—a mechanism called dependency checking.

The beauty of the make command is its flexibility. You can use make with a simple make, or you can write complex makefiles that contain numerous macros, rules, or commands that work in a single directory or traverse your filesystem recursively to build programs, update your system, and even function as document management systems. The make works with nearly any program, including text processing systems such as Tex.

You use make like this:

```
# make install
```

You can use the default Makefile, or you can use make's -f option to specify any makefile, such as MyMakefile, like this:

```
# make -f MyMakefile
```