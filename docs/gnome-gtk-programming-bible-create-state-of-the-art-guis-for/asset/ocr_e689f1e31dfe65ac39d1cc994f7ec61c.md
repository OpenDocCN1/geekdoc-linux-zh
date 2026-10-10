The list of commands for clean can be anything - just as you would enter it from the command line. It is common to have special labels in make files for things such as make install (to copy files to other locations) or make force (which does a clean followed by a recompile).

![](bbox=[0.03, 0.24, 0.14, 0.27])

The make utility originated in the early days of UNIX and has some quirks left over from those early days. The one that is most likely to trip you up is that the tab character is part of the syntax. The two rm statements in the previous example must be indented by tabs, not simply spaces. If you get some kind of strange error message out of make, then check your tabs. Missing tabs can cause make to misinterpret a statement and issue an error message for what it thought it had found.

Here is another make file that does exactly the same thing as the previous one, but is a bit more explicit:

```
CC=gcc
LDFLAGS=-lm
CFLAGS=-Wall -g

helloworld2: helloworld2.o helloworld2.o hellomath.o
$ (CC) $(LDFLAGS) helloworld2.o hellomath.o -o helloworld2

helloworld2.o: helloworld2.c
$ (CC) $(CFLAGS) -c helloworld2.c

hellomath.o: hellomath.c
$ (CC) $(CFLAGS) -c hellomath.c

clean:
rm -f helloworld2
rm -f *.o
```

Here the LDLIBS is set just as it was in the previous example, but the arguments to the linker are specified instead of being allowed to default. The commands used to compile the two source modules also are specified, and they use the variable named CFLAGS to pass arguments to gcc. The -Wall option tells the compiler to issue a warning for anything it finds - even some that work but are considered bad coding practices. This option is used in all the examples in this book to make sure the code is as clean as possible. The -g option causes debugging information to be compiled in with the code and you can use a symbolic debugger on the program. If you use this, you will want to remove the debugging information before you put the program into production since it causes the object files to be very large. You can remove the debug information from an object file with strip, or you can remove -g from CFLAGS and compile everything again.

There is a lot more to make than described here, but this is enough to get started compiling and linking programs. Some of the other things, such as linking with third-party libraries and establishing dependencies on header files, will pop up here and there. The make files in this book are as simple as is reasonably possible.