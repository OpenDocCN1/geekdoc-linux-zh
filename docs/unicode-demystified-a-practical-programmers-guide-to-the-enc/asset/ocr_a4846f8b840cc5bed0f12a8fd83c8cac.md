# $ cat testtabs
xyzTababc

# Avoid Using Optimization Flags with the Debugger

Limit the optimization flags to -O or -O2 when you compile a program for debugging. Because debugging and optimizing inherently have different goals, it may be best to avoid combining the two.

You cannot specify the input file to tabs when you first call the debugger. Specify the input file once you have called the debugger and started execution with the run command.

To run the debugger on the sample executable, give the name of the file on the command line when you run gdb. You will see some introductory statements about gdb, followed by the gdb prompt (gdb). The debugger is ready to accept commands. The list command displays the first ten lines of source code:

```
$ g tabs
GNU 4.18
Copyright 1998 Free Software Foundation, Inc.
GDB is free postsoft, covered by the GNU General Public License and you are welcome to change it and/or distribute copies of it under certain conditions.
Type "show copying" to see the conditions.
There is absolutely no warranty for GDB. This GDB was configured as "i386-redhat-linux"
```

```
(gdb) list
#include <stdio.h>
#define TABSIZE 8
/* prototype for function findstop */
int findstop(int *);

int main(void) 
{
    int c; /* character read from stdin */
    int posn = 0; /* column position of character */
    int inc; /* column increment to tab stop */
    while ((c = getchar()) != EOF)
        switch (c)
            case '\t': /* c is a tab * */
                inc = findstop(&posn);
                for(; inc > 0; inc--)
                    putchar(' ');
            break;
```