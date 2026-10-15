
target-list: dependency-list
Or
target-list:: dependency-list
<Tab> command-list

Purpose: The syntax of a make rule

Here, target-list is a list of target files separated by one or more spaces, dependency-list is a list of files (object, header, source code, etc.) separated by one or more spaces that the target files depend on, and command-list is a list of commands—separated by the newline character—that have to be executed to create the target files. Each command in the command-list starts with the <Tab> character. The comment lines start with the # character. Files in the target-list and dependency-list may use shell wildcards ?, *, [, and {}.

With the : operator, a target is considered out of date if its modification time is less than any of the files in the dependency-list. If the operator is !, the target is always recreated after examining and recreating the sources in the dependency-list. With the :: operator, the targets are always recreated if no sources are specified in dependency-list. In case of the : and ! operator, the target is removed if make is interrupted, but not in case of the :: operator. In this book, we use only the most commonly used : operator.

The makefile consists of a list of make rules that describe the dependency relationships between files that are used to create an executable file. The make utility uses the rules in the makefile to determine which of the files that comprise your program need to be recompiled and relinked to recreate the executable. Thus, for example, if you modify a header (.h) file, the make utility recompiles all those files that include this header file. The files that contain this header file must be specified in the corresponding makefile.

The following makefile can be used for the power program discussed in Section 17.5.3.

```
% cat makefile
# Sample makefile for the power program
# Remember: each command line starts with a <TAB>
power: power.c
	cc power.c -o power -lm
%
```

If the executable file power exists and the source file power.c has not been modified since the executable file was created, running make will give the message that the executable file is up to date for power.c. Therefore, make has no need to recompile and relink power.c. At times, you will need to force the remaking of an executable because, for example, one of the system header files included in your source has changed. In order to force recreation of the executable, you will need to change the last update time. One commonly used method for doing so is to use the touch command, and rerun make. The following session illustrates these points.

```
% make
make: 'power' is up to date.
```

```
% touch power.c
% make
cc power.c -o power -lm
%
```

When you use the touch command with one or more existing files as its arguments, it sets their last update time to the current time. When used with a nonexistent file as an argument, it creates a zero-length (i.e., empty) file with that name.

In the following in-chapter exercise, you will use the make command to create an executable for a single source file.

## EXERCISE 17.3

Create the executable code for the C program in the power.c file and place it in a file called XpowerY. Use the make utility to perform this task by using the makefile given previously. Run XpowerY to confirm that the program works properly.

In order to show a next-level use of the make utility, we partition the C program in the power.c file into two files: power.c and compute.c. The following session shows the contents of these files. The compute.c file contains the compute function, which is called from the main function in power.c. To generate the executable in the power file, we need to compile the two source files independently and then link them, as shown in the two cc command lines at the end of the session.

```
% cat power.c
#include <stdio.h>

double compute(double x, double y);
int main()
{
    float   x,y;
    printf ("The program takes x and y from stdin and
    displays x^y.\n");
    printf ("Enter integer x: ");
    scanf ("%f", &x);
    printf ("Enter integer y: ");
    scanf ("%f", &y);
    printf ("x^y is: %6.3f\n", compute(x,y));
}
% cat compute.c
#include <math.h>
double compute (double x, double y)
{
    return (pow ((double) x, (double) y));
}
```
