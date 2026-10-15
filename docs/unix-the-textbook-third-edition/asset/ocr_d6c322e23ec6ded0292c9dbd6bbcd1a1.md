You simply have to learn to ignore such messages. The following is a brief description of the lint utility.

# SYNTAX

```
lint [options] file-list
```

Purpose: Allows checking of C programs, specified in file-list, for features that can be bugs, nonportable, or wasteful of system resources

# Commonly used options/features:

+   -c Check type casts (coercions) of questionable validity
+   -s Produce one-line error messages (or warnings) only
+   -u Suppress complaints about external variables and functions used and not defined, or vice versa; useful for running lint on a subset of modules of a software
+   -v Suppress complaints about unused arguments in functions

We demonstrate the use of lint with the simple program shown in the following session and stored in the cat.c file. The program reads input from stdin and sends it to stdout. It is in a sense, then, a simple version of the cat command. We have used the nl command with -ba option to number all the source lines (including blank lines) because the line numbers reported in lint's error messages include blank lines.

```
% nl -ba cat.c
     1   /* Copy stdin to stdout */
     2
     3   #include <stdio.h>
     4
     5   int main(int argc, char *argv[])
     6   {
     7       char c;
     8       int     i, j;
     9
    10       while ((c=getchar()) != EOF)
    11           putchar(c);
    12   }
%
```

The program compiles without any error messages from the compiler. It also runs without a problem, echoing each line entered from the keyboard until you press <Ctrl+D>, the EOF character in UNIX on a new line. The compilation and execution of the program is shown in the following session.

```
% a.out
Hello there!
Hello there!
Let's see how it goes.
```