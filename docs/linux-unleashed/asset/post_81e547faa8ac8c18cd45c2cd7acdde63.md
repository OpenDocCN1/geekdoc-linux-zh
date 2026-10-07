
# **NOTE**

makefile or Makefile is literally the name that the make program expects to find in the current directory. You can override the name if you want, but tradition (and who can argue with 30 years of tradition?) dictates that makefile is the name programmers should use.

make is certainly best suited for C programming, but it can also be used with other types of language compilers for Linux, such as assembler or FORTRAN.

## A Sample makefile

Let's look at a simple application of make. The command

```
$ make someonehappy
```

tells Linux that you want to create a new version of someonehappy. In this case, someonehappy is an executable program; thus, there will be compiling and linking of files. someonehappy is referred to as the target of this make operation. The object files that are linked together to create the executable are known as someonehappy's dependents. The source code files that are compiled to create these object files are also indirect dependents of someonehappy.

The files that are used to build someonehappy are the following (the contents of these files are unimportant to the example):

- Two C source code files: main.c, dothis.c
- Three header files: yes.h, no.h, maybe.h
- One library file: /usr/happy/lib/liketree.a
- An assembly language file: itquick.s

It appears that this is a small project, so you could choose to manually compile and link these files to build your executable. Instead, create a makefile for your someonehappy project to help automate these tedious tasks.

In your favorite editor, write the following:

```
someonehappy: main.o dothis.o itquick.o /usr/happy/lib/liketree.a
       cc -o someonehappy main.o dothis.o itquick.o /usr/happy/lib/
       -liketree.a
main.o: main.c
       cc -c main.c
dothis.o: dothis.c
       cc -c dothis.c
itquick.o: itquick.s
       as -o itquick.o itquick.s
fresh:
       rm *.o
maybe.h: yes.h no.h
       cp yes.h no.h /users/sue/
```

## Basic makefile Format

So, assuming that these files are in the same directory as the *makefile*, what do you have? The format of a *makefile*, such as the one you have made, is a series of entries. Your *makefile* has six entries. The first line of an entry is the dependency line, which lists the dependencies of the target denoted at the left of the colon; the second line is one or more command lines, which tells *make* what to do if the target is newer than its dependent (or dependents). An entry basically looks like this:

```
target: dependents
    command list
```

The space to the left of the *command list* is actually a tab. This is part of the *makefile* syntax: Each command line must be indented using a tab. A dependency line can have a series of commands associated with it. *make* executes each command line as if the command had its own shell. Thus, the command

```
cd somewhere
mv *.c anotherwhere
```

does not behave the way you may have intended. To remedy this kind of situation, use the following syntax whenever you need to specify more than one command:

```
dependency line
command1;command2;command3;...
```

or

```
dependency line
    command1; \
    command2; \
    command3;
```

and so on. If you use a backslash to continue a line, it must be the last character before the end-of-line character.

# **TIP**

You can specify different kinds of dependencies for a target by placing the same target name on different dependency lines. Actually, make is even more powerful than described in this chapter, but unless you are working on very large projects with lots of interdependencies, you probably won't care about most of the subtleties make is capable of.

The first entry in our makefile is the key one for building our executable. It states that someonehappy is to be built if all the dependent object files and library files are present and if there are any newer files than the last version of someonehappy. Of course, if the executable is not present at all, make performs the compile command listed, but not right away. First, make checks to see which object files need to be recompiled in order to recompile someonehappy. This is a recursive operation, as make examines the dependencies of each target in the hierarchy, as defined in the makefile.

The last entry is a little goofy. It copies the header files yes.h and no.h (somehow related to maybe.h) to the home directories of the user named sue if they have been modified. This is somewhat conceivable if Sue is working on related programs that use these header files and need the most recent copies at all times. More importantly, it illustrates that make can be used to do more than compiling and linking and that make can execute several commands based on one dependency.

The fresh target is another example of a target being used to do more than just compiling. This target lacks any dependents, which is perfectly acceptable to the make program. As long as there is no file in the current directory named fresh, make executes the supplied command to remove all object files. This works because make treats any such entry as a target that must be updated.

So, if you enter the command

```
$ make someonehappy
```

make starts issuing the commands it finds in the makefile for each target that must be updated to achieve the final target. make echoes these commands to the user as it processes them. Simply entering

```
$ make
```

also works in this case because make always processes the first entry it finds in the makefile. These commands are echoed to the screen, and the make process halts if the compiler finds an error in the code.

If all of someonehappy's dependencies are up-to-date, make does nothing except inform you of the following:

```
'someonehappy' is up to date
```

You can actually supply the name (or names) of any valid target in your makefile on the command line for make. It performs updates in the order in which they appear on the command line, but still applies the dependency rules found in the makefile. If you supply the name of a fictional target (one that doesn't appear in your makefile and is not the name of a file in the current directory), make complains something like this:

```
$ make fiction
make: Don't know how to make fiction. Stop.
```

## Building Different Versions of Programs

Suppose you want to have different versions of your someonehappy program that use most of the same code, but require slightly different interface routines. These routines are located in different C files (dothis.c and dothat.c), and they both use the code found in main.c. Instead of having separate makefiles for each version, you can simply add targets that do different compiles. Your makefile will look like the following one. (Note the first line that has been added. It is a comment about the makefile and is denoted by a # character followed by the comment text.)

```
# A makefile that creates two versions of the someonehappy program
someonehappy1: main.o dothis.o itquick.o /usr/happy/lib/liketree.a
      cc -o someonehappy main.o dothis.o itquick.o /usr/happy/lib/liketree.a
someonehappy2: main.o dothat.o itquick.o /usr/happy/lib/liketree.a
      cc -o someonehappy main.o dothat.o itquick.o /usr/happy/lib/liketree.a
main.o: main.c
      cc -c main.c
dothis.o: dothis.c
      cc -c dothis.c
dothat.o: dothat.c
      cc -c dothat.c
itquick.o: itquick.s
      as -o itquick.o itquick.s
fresh:
      rm *.o
maybe.h: yes.h no.h
      cp yes.h no.h /users/sue/
```

Thus, your makefile is now equipped to build two variations of the same program. Issue the command

```
$ make someonehappy1
```

to build the version using the interface routines found in `dothis.c`. Build your other program that uses the `dotdot.c` interface routines with the following command:

```
$ make someonehappy2
```

## Forcing Recompiles

It is possible to trick `make` into doing (or not doing) recompiles. An example of a situation in which you may not want `make` to recompile is when you have copied files from another directory. This operation updates the modification times of the files, though they may not need to be recompiled. You can use the `touch` utility or `make` with the `-t` option to update the modification times of all target files defined in the `makefile`.

> **TIP**

Do you want to test your `makefile`? Use `make` with the `-n` option. It will echo the commands to you without actually executing them. Any coding errors written into the file generate proper error messages from the parser, but you won't have to wait for a compiler to complete its task.

## Macros

`make` lets you define macros within your `makefile` which are expanded by `make` before the program executes the commands found in your `makefile`. Macros have the following format:

```
macro identifier = text
```

The text portion can be the name of a file, a directory, a program to execute, or just about anything. Text can also be a list of files or a literal text string enclosed by double quotes. The following is an example of macros that you might use in your `someonehappy` `makefile`:

```
LIBFILES=/usr/happy/lib/liketree.a
objects = main.o dothis.o
CC = /usr/bin/cc
1version="This is one version of someonehappy"
OPTIONS =
```

As a matter of convention, macros are usually in uppercase, but they can be typed in lowercase as in the previous example. Notice that the `OPTIONS` macro defined in the list has no text after the equal sign. This means that you have assigned the `OPTIONS` macro to
