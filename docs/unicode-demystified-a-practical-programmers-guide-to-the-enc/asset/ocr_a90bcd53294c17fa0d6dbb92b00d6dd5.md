The language accepted by the GNU C compiler includes features that are not of the ANSI standard for the language. Using this option forces gcc to reject these language extensions and accept only standard programming language features.

-traditional Causes gcc to accept only C programming language features that existed in the traditional Kernighan and Ritchie C programming. This option allows you to compile correctly older programs using the traditional C language that existed before the ANSI standard C language was defined.

-Dname=value Usually #define preprocessor directives are given in header, or include, files. You can use this option to define symbolic names on the command line. For example, -DLux is equivalent to having the line #define Linux in an include file, and -DMACH=i586 is the same as #define MACH i586.

-fpic Causes gcc to produce position-independent code, which is suitable for installing a shared library.

-twirl-strings By default, the GNU C compiler places strings into protected memory, where they cannot be changed. Some (usually older) programs assume that you can modify string constants. This option changes the behavior of gcc so string constants can be modified.

# Notes

The preceding list of options is only a small fraction of the full set of options available with the GNU C compiler. See the gcc option info page for a complete list.
Although the -o option is generally used to specify a filename to store object code, this option can also be used to use name files resulting from other compilation steps. In the following example the -o option causes the assembly language produced by the following gcc command to be stored in the file acode instead of pgm.s.

```
$ gcc -S -o code pgm.c
```

The lint utility found in many UNIX systems is not available on GNU/Linux. However, the -Wall option performs many of the same checks and can be used in place of lint (page 859).

The conventions used by the C compiler for assigning filename extensions are summarized in Table III-18.

# Examples

The first example compiles, assembles, and links a single C program, compute.c. The executable output is put in a.out. The gcc utility deletes the object file:

```
$ gcc compute.c
```