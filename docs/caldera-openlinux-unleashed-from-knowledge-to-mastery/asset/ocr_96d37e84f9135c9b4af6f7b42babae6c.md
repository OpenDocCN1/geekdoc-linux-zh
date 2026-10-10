C is popular because of a number of factors:

+   * It features a wide variety of data types, operators, and library functions for dealing with many common programming tasks.
+   * C is a fairly low-level language and can be translated into very efficient machine code.
+   * C is standardized (ANSI standard X3.159-1989 and a corresponding ISO standard). This means that if you follow the standard, your C programs are likely to be portable to a wide variety of operating systems and architectures.
+   * C is a fairly small language. It has only about 32 reserved words and a simple and consistent syntax.

**Note**

Some would argue about the simplicity of the syntax. Complicated type declarations can, in fact, be quite murderous to disentangle. But mostly C is quite readable.

+   * There are many implementations of C for a wide variety of machines.

C has had many dialects that lead to the push to standardize C. In my opinion, the ANSI standardization committee has done an excellent job and produced a consistent, understandable language definition. I discuss only ANSI standard C in this chapter; pre-ANSI dialects will not be considered here.

# “Hello, World” in C

For some reason, almost all introductions to C present a program that prints “Hello, World” on the terminal. I will continue this strong tradition and present the canonical “Hello, World” C program.

```
/* Canonical first C program */
#include <stdio.h>

int main()
{
    printf("Hello, World\n");
    return 0;
}
```