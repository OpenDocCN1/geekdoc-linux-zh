+   Shared Library—A shared library is a collection of object code that is dynamically linked at runtime. For example, the C standard library is found in a shared library (//lib/libc.so.6.) This code is linked in by the runtime loader when a program that needs it is started.

The great advantages of shared libraries are that executable files are much smaller—the library code does not have to be statically linked into the executable—and multiple programs all share the same library code, saving memory at runtime.

# # The GNU C Compiler

The GNU C Compiler (gcc) was the first major project of the Free Software Foundation. It was written originally by Richard Stallman, and is now maintained by Cygnus Solutions. gcc exists for practically all major operating systems and processor architectures and is widely used in embedded systems. It is also the native C and C++ compiler on Linux.

gcc conforms to the ANSI C standard and g++ (the C++ compiler) tracks the proposed ANSI C++ standard. Both compilers are documented in the gcc info page.

# ## Invoking gcc

The gcc command, commonly is used to compile a C source files, gcc has dozens of options, but in this chapter, I only cover the more common ones.

Let’s start with the simplest case—a C program entirely contained in a single C source file. To compile such a file into an executable, invoke gcc like this:

```
$ gcc -o executable_name source_name.c
```

The preceding example compiles source_name.c and links it with the C runtime library to produce the executable file executable_name.

Most non-trivial C programs are split into more than one source file. To create executables from these programs, you need to compile (but not link) each source file separately, and then link the final object files together. To compile a source file into an object file without performing linking, use the -c option:

```
$ gcc -c -o obj_file.o source_file.c
```

Suppose you have two source files, main.c and helper.c. To compile and link them to form an executable, use these commands:

```
$ gcc -c -o main.o main.c
$ gcc -c -o helper.o helper.c
$ gcc -o program main.o helper.o
```