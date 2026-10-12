at that line and run gdb. When the line is reached, execution is interrupted. You can check variable values, examine the stack trace, and observe the program's environment. You can single-step through the program to check values. You can resume execution at any point. By using breakpoints, you can discover many bugs in code.

A graphical X Window System interface to gdb is called the Data Display Debugger, or Gdb.

# Using the GNU C Compiler

If you elected to install the development tools package when you installed Fedora Core (or perhaps later on, using RPM, or other package tools), you should have the GNU C compiler (*gcc*). Many different options are available for the GNU C compiler, and many of them are similar to those of the C and C++ compilers that are available on other UNIX systems. Look at the man page or information file for *gcc* for a full list of options and descriptions.

When you build a C program using *gcc*, the compilation process takes place in several steps:

+   1. First, the C preprocessor parses the file: To do so, it sequentially reads the lines, includes header files, and performs macro replacement.

+   2. The compiler parses the modified code to determine whether the correct syntax is used. In the process, it builds a symbol table and creates an intermediate object format. Most symbols have specific memory addresses assigned, although symbols defined in other modules, such as external variables, do not.

+   3. The last compilation stage, linking, ties together different files and libraries and then links the files by resolving the symbols that had not previously been resolved.

> Most C programs compile with a C++ compiler if you follow strict ANSI rules. For example, you can compile the standard *hello.c* program (everyone's first program) with the GNU C++ compiler. Typically, you name the file something like *hello.c*, *hello.cc*, *hello.c++*, or *hello.cxx*. The GNU C++ compiler accepts any of these names.

# A Simple C Program

This section provides a simple example of how to create an executable program for Linux by using *gcc*. One of the shortest programs you can write in C for Linux is the quintessential "hello, world" program (popularized by Brian W. Kernighan and Dennis M. Ritchie in their 1978 book *The C Programming Language*).