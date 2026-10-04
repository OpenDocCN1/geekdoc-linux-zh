# 726 Exploring the Software Development Tools in Fedora Core

To ensure the executable is properly prepared for debugging, use the -g option with GCC. You can do this task by defining the variable CFLAGS in your makefile

```
CFLAGS= -g
```

# Running gdb

The most common way to debug a program is to run gdb by using the following command:

gdb progname is the name of the program's executable. After it run, gdb displays the following message and prompts you for a command:

GNU Red Hat Linux (6.0.0-2.20031117.rh1)
Copyright 2003 Free Software Foundation, Inc.
GDB is free software, covered by the GNU General Public License, and you are welcome to change and/or distribute copies of it under certain conditions.
Type "show copying" to see the conditions.
There is absolutely no warranty for GDB. Type "show warranty" for details.
This GDB was configured as "i386-redhat-linux-gnu".
(gdb)

You can type gdb commands at the (gdb) prompt. One useful command is
-- help it displays a list of commands as the next lists showing:

+   (gdb) help
List of classes of commands:
- data Examining data
- files Specifying and examining files
- aliases Aliases of other commands
- breakpoints Making program stop at certain points
- internals Maintenance commands
- obscure obscure features
- running Running the program
- stack Examining the stack
- status Status inquiries
- support Support facilities
- tracepoints Tracing of program execution without stopping the program
- user-defined User-defined commands

Type "*" followed by a class name for a list of commands in that class.
Type "*" followed by command name for full documentation.
Command name abbreviations are allowed if unambiguous.
(gdb)

To quit gdb, q and press Enter.

gdb has a large number of commands, but you only need one to find the cause of an error quickly. Table 1-4 lists the commonly used gdb commands.