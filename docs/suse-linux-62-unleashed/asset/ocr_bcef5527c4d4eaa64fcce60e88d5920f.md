# Project Management Tools

This section introduces some of the programming and project management tools included with SuSE Linux. You'll find numerous programs on this book's CD-ROM that you can use to help automate your software projects. If you have some previous UNIX experience, you'll be familiar with most of these programs because they are traditional complements to a programmer's suite of software.

If you have programming experience on other software platforms, you'll find that these programs are easy to learn. However, mastery will come with experience!

# Building Programs with make

The make command is only one of several programming automation utilities included with SuSE Linux. You'll find others, as pnake (the BSD make), make (a template-based makefile generator, usually for building X11 applications), autotake, and autoconf (which builds shell scripts to configure program source code packages).

> For a bit more information about make and building makefiles when developing Motif clients for the X Window System, see the section "Motif Programming," later in the chapter.

The make command's roots stem from an early version of System V UNIX. The version included with SuSE Linux is part of the GNU utilities distribution. make is used to automatically handle the building and install of a program, which can be as simple as

```
# make install
```

The magic of make is that it will automatically update and build applications. You create this magic through a default file named Makefile. However, if you use make's -f option, you can specify any Makefile, such as MyMakefile, like this:

```
# -f MyMakefile
```

A Makefile is a text file that can contain instructions about which options to pass to the compiler preprocessor, the compiler, and the linker. The Makefile can also specify which source files need to be compiled (and the compiler command line) for a particular code module, and which code modules are needed to build the program—a mechanism called dependency checking.

![](bbox=[0.859, 0.796, 0.958, 0.933])