the GNU C++ compiler. Typically, you will name the file something like `hello.cc`, `hello.C`, `hello.c++`, or `hello.cxx`. The GNU C++ compiler will accept any of these names.

# # Project Management Tools

This section introduces some of the programming and project management tools included with Red Hat Linux. You will find tools on this book’s CD-ROMS that you can use to help automate your software development projects. If you have some previous UNIX experience, you will be familiar with most of these programs because they are traditional complements to a programmer’s suite of software.

If you have programming experience on other software platforms, you will find that these programs are easy to learn. However, mastery will come with experience!

# ## Building Programs with make

The `make` command is only one of several programming automation utilities included with Red Hat Linux. You will find others, such as `pmake` (a parallel make), `smake` (a dependency-drive Makefile generator, usually for building X11 applications), `automake`, and one of the newer tools, `autoconf` (which builds shell scripts used to configure program source code packages). Check the man pages for more information.

The `make` command’s roots stem from an early version of System V UNIX. The version included with Red Hat Linux is part of the GNU utilities distribution. `Make` is used to automatically handle the building and install of a program, which can be as simple as

```
```
# make install
```
```

The magic of `make` is that it will automatically update and build applications. You create this magic through a default file named `Makefile`. However, if you use `make`’s `-f` option, you can specify any Makefile, such as `MyMakeFile`, like this:

```
```
# make -f MyMakeFile
```
```

A Makefile is a text file that can contain instructions about which options to pass on to the compiler preprocessor, the compiler, and the linker. The Makefile can also specify which source code files need to be compiled (and the compiler command line) for a particular code module, and which code modules are needed to build the program—a mechanism called *dependency checking*.

Using `make` can also aid in the portability of your program through the use of macros. This allows users of other operating systems to easily configure a program build by specifying local values, such as the names and locations, or *pathnames* of any required