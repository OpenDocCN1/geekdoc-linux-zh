
```
#include <unistd.h>
```

These also refer to header files, but they refer to header files that live outside the current source tree. They are supplied by the system to support the compilation of every program. If we look in /usr/include, we can see them:

```
[me@linuxbox diction-1.11]$ ls /usr/include
```

The header files in this directory were installed when we installed the compiler.

## Building The Program

Most programs build with a simple two command sequence:

```
./configure
make
```

The configure program is a shell script which is supplied with the source tree. Its job is to analyze the build environment. Most source code is designed to be portable. That is, it is designed to build on more than one kind of Unix-like system. But in order to do that, the source code may need to undergo slight adjustments during the build to accommodate differences between systems. configure also checks to see that necessary external tools and components are installed. Let’s run configure. Since configure is not located where the shell normally expects programs to be located, we must explicitly tell the shell its location by prefixing the command with ./ to indicate that the program is located in the current working directory:

```
[me@linuxbox diction-1.11]$ ./configure
```

configure will output a lot of messages as it tests and configures the build. When it finishes, it will look something like this:

```
checking libintl.h presence... yes
checking for libintl.h... yes
checking for library containing gettext... none required
configure: creating ./config.status
```

```
config.status: creating Makefile
config.status: creating diction.1
config.status: creating diction.texi
config.status: creating diction.spec
config.status: creating style.1
config.status: creating test/rundiction
config.status: creating config.h
[me@linuxbox diction-1.11]$
```

What’s important here is that there are no error messages. If there were, the configuration failed, and the program will not build until the errors are corrected.

We see configure created several new files in our source directory. The most important one is Makefile. Makefile is a configuration file that instructs the make program exactly how to build the program. Without it, make will refuse to run. Makefile is an ordinary text file, so we can view it:

```
[me@linuxbox diction-1.11]$ less Makefile
```

The make program takes as input a makefile (which is normally named Makefile), which describes the relationships and dependencies among the components that comprise the finished program.

The first part of the makefile defines variables that are substituted in later sections of the makefile. For example we see the line:

```
CC=           gcc
```

which defines the C compiler to be gcc. Later in the makefile, we see one instance where it gets used:

```
diction:       diction.o sentence.o misc.o getopt.o getopt1.o
              $(CC) -o $@ $(LDFLAGS) diction.o sentence.o misc.o \
              getopt.o getopt1.o $(LIBS)
```

A substitution is performed here, and the value $(CC) is replaced by gcc at run time.

Most of the makefile consists of lines, which define a target, in this case the executable file diction, and the files on which it is dependent. The remaining lines describe the command(s) needed to create the target from its components. We see in this example that

the executable file diction (one of the final end products) depends on the existence of diction.o, sentence.o, misc.o, getopt.o, and getopt1.o. Later on, in the makefile, we see definitions of each of these as targets:

```
diction.o:      diction.c config.h getopt.h misc.h sentence.h
getopt.o:      getopt.c getopt.h getopt_int.h
getopt1.o:     getopt1.c getopt.h getopt_int.h
misc.o:        misc.c config.h misc.h
sentence.o:    sentence.c config.h misc.h sentence.h
style.o:       style.c config.h getopt.h misc.h sentence.h
```

However, we don't see any command specified for them. This is handled by a general target, earlier in the file, that describes the command used to compile any .c file into a .o file:

```
.c.o:
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $<
```

This all seems very complicated. Why not simply list all the steps to compile the parts and be done with it? The answer to this will become clear in a moment. In the meantime, let's run make and build our programs:

```
[me@linuxbox diction-1.1]$ make
```

The make program will run, using the contents of Makefile to guide its actions. It will produce a lot of messages.

When it finishes, we will see that all the targets are now present in our directory:

```
[me@linuxbox diction-1.1]$ ls
config.guess  de.po        en           install-sh   sentence.c
config.h      diction       en_GB        Makefile     sentence.h
config.h.in   diction.1     en_GB.mo     Makefile.in  sentence.o
config.log    diction.1.in  en_GB.po     misc.c       style
config.status diction.c     getopt1.c    misc.h       style.1
config.sub    diction.o     getopt1.o    misc.o       style.1.in
configure     diction.pot   getopt.c     NEWS         style.c
configure.in  diction.spec  getopt.h     nl           style.o
COPYING       diction.spec.in getopt_int.h nl.mo        test
de            diction.texi  getopt.o     nl.po
```
