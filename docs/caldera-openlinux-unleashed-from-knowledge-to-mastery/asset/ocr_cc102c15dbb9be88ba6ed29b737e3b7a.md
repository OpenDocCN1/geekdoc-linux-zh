# Compiling C++ Programs

To compile and link C++ programs, you should invoke the compiler as g++ rather than gcc. This is especially important at link time because it forces the linker to link in certain libraries required by C++ programs.

# GNU Make

Any non-trivial C or C++ project has several (probably many) source files and headers. If you edit a source file, you need to rebuild the project. There are several approaches you can take:

+   * When you change something, you can recompile and relink everything. This is very slow and wasteful.
+   * When you change something, you can enter the commands needed to compile the parts of the project that need recompilation. This is efficient, but tedious and error-prone.
+   * You can use make to keep track of dependencies and automatically rebuild those parts of the project which need rebuilding.

Clearly, the make approach is the best.

# Makefiles

The make program reads a special file called a Makefile. This file contains a list of targets and dependencies. It also contains rules specifying which commands should be run if a target needs to be rebuilt.