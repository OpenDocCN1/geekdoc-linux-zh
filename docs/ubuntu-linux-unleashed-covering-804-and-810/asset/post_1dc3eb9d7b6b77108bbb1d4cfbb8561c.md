
## Building Programs with make

You use the make command to automatically build and install a C program, and for that use, it is an easy tool. If you want to create your own automated builds, however, you need to learn the special syntax that make uses; the following sections walk you through a basic make setup.

### Using Makefiles

The make command automatically builds and updates applications by using a makefile. A makefile is a text file that contains instructions about which options to pass on to the compiler preprocessor, the compiler, the assembler, and the linker. The makefile also specifies, among other things, which source code files have to be compiled (and the compiler command line) for a particular code module and which code modules are needed to build the program—a mechanism called dependency checking.

The beauty of the make command is its flexibility. You can use make with a simple makefile, or you can write complex makefiles that contain numerous macros, rules, or commands that work in a single directory or traverse your file system recursively to build programs, update your system, and even function as document management systems. The make command works with nearly any program, including text processing systems such as TeX.

You could use make to compile, build, and install a software package, using a simple command like this:

```
# make install
```

You can use the default makefile (usually called Makefile, with a capital M), or you can use make's -f option to specify any makefile, such as MyMakeFile, like this:

```
# make -f MyMakeFile
```

Other options might be available, depending on the contents of your makefile.

### Using Macros and Makefile Targets

Using make with macros can make a program portable. Macros allow users of other operating systems to easily configure a program build by specifying local values, such as the names and locations, or pathnames, of any required software tools. In the following example, macros define the name of the compiler (CC), the installer program (INS), where the program should be installed (INSDIR), where the linker should look for required libraries (LIBDIR), the names of required libraries (LIBS), a source code file (SRC), the intermediate object code file (OBJS), and the name of the final program (PROG):

```
# a sample makefile for a skeleton program
CC= gcc
INS= install
INSDIR = /usr/local/bin
LIBDIR= -L/usr/X11R6/lib
LIBS= -lXm -lSM -lICE -lXt -lX11
SRC= skel.c
OBJS= skel.o
PROG= skel

skel: $(OBJS)
	$(CC) -o $(PROG) $(SRC) $(LIBDIR) $(LIBS)

install: $(PROG)
	$(INS) -g root -o root $(PROG) $(INSDIR)
```

**NOTE**

The indented lines in the previous example are indented with tabs, not spaces. This is important to remember! It is difficult for a person to see the difference, but make can tell. If make reports confusing errors when you first start building programs under Linux, check your project's makefile for the use of tabs and other proper formatting.

Using the makefile from the preceding example, you can build a program like this:

```
# make
```

To build a specified component of a makefile, you can use a target definition on the command line. To build just the program, you use make with the skel target, like this:

```
# make skel
```

If you make any changes to any element of a target object, such as a source code file, make rebuilds the target automatically. This feature is part of the convenience of using make to manage a development project. To build and install a program in one step, you can specify the target of install like this:

```
# make install
```

Larger software projects might have a number of traditional targets in the makefile, such as the following:

- test—To run specific tests on the final software
- man—To process an nroff or a troff document with the man macros
- clean—To delete any remaining object files
- archive—To clean up, archive, and compress the entire source code tree
- bugreport—To automatically collect and then mail a copy of the build or error logs

Large applications can require hundreds of source code files. Compiling and linking these applications can be a complex and error-prone task. The make utility helps you organize
