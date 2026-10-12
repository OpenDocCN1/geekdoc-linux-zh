
To ensure that the executable is properly prepared for debugging, use the `-g` option with GCC. You can do this task by defining the variable `CFLAGS` in the makefile as

```
CFLAGS= -g
```

# **Running `gdb`**

The most common way to debug a program is to run `gdb` by using the following command:

```
gdb `progname`
```

`progname` is the name of the program’s executable file. After it runs, `gdb` displays the following message and prompts you for a command:

```
GNU gdb Red Hat Linux (6.0post-0.20031117.7rh)
Copyright 2003 Free Software Foundation, Inc.
GDB is free software, covered by the GNU General Public License, and you are
welcome to change it and/or distribute copies of it under certain conditions.
Type "Show copying" to see the conditions.
There is absolutely no warranty for GDB. Type "show warranty" for details.
This GDB was configured as "i386-redhat-linux-gnu".
(gdb)
```

You can type `gdb` commands at the `(gdb)` prompt. One useful command is `help` — it displays a list of commands as the next listing shows:

```
(gdb) help
List of classes of commands:

aliases -- Aliases of other commands
breakpoints -- Making program stop at certain points
data -- Examining data
files -- Specifying and examining files
internals -- Maintenance commands
obscure -- Obscure features
running -- Running the program
stack -- Examining the stack
status -- Status inquiries
support -- Support facilities
tracepoints -- Tracing of program execution without stopping the program
user-defined -- User-defined commands
```

```
Type "help" followed by a class name for a list of commands in that class.
Type "help" followed by command name for full documentation.
Command name abbreviations are allowed if unambiguous.
(gdb)
```

To quit `gdb`, type `q` and then press Enter.

`gdb` has a large number of commands, but you need only a few to find the cause of an error quickly. Table 1-4 lists the commonly used `gdb` commands.

# Table 1-4 Commonly Used gdb Commands

| This Command | Does the Following |
| :--- | :--- |
| break NUM | Sets a breakpoint at the specified line number (the debugger stops at breakpoints). |
| bt | Displays a trace of all stack frames. (This command shows you the sequence of function calls so far.) |
| clear FILENAME:NUM | Deletes the breakpoint at a specific line in a source file. For example, clear xdraw.c:8 clears the breakpoint at line 8 of file xdraw.c. |
| continue | Continues running the program being debugged. (Use this command after the program stops due to a signal or breakpoint.) |
| display EXPR | Displays the value of expression (consisting of variables defined in the program) each time the program stops. |
| file FILE | Loads a specified executable file for debugging. |
| help NAME | Displays help on the command named NAME. |
| info break | Displays a list of current breakpoints, including information on how many times each breakpoint is reached. |
| info files | Displays detailed information about the file being debugged. |
| info func | Displays all function names. |
| info local | Displays information about local variables of the current function. |
| info prog | Displays the execution status of the program being debugged. |
| info var | Displays all global and static variable names. |
| kill | Ends the program you're debugging. |
| list | Lists a section of the source code. |
| make | Runs the make utility to rebuild the executable without leaving gdb. |
| next | Advances one line of source code in the current function without stepping into other functions. |
| print EXPR | Shows the value of the expression EXPR. |
| quit | Quits gdb. |
| run | Starts running the currently loaded executable. |
| set variable VAR=VALUE | Sets the value of the variable VAR to VALUE. |
| shell CMD | Executes a UNIX command CMD without leaving gdb. |
| step | Advances one line in the current function, stepping into other functions, if any. |
| watch VAR | Shows the value of the variable named VAR whenever the value changes. |
| where | Displays the call sequence. Use this command to locate where your program died. |
| x/F ADDR | Examines the contents of the memory location at address ADDR in the format specified by the letter F, which can be o (octal); x (hex); d (decimal); u (unsigned decimal); t (binary); f (float); a (address); i (instruction); c (char); or s (string). You can append a letter indicating the size of data type to the format letter. Size letters are b (byte); h (halfword, 2 bytes), w (word, 4 bytes); and g (giant, 8 bytes). Typically, ADDR is the name of a variable or pointer. |

# *Finding bugs by using gdb*

To understand how you can find bugs by using *gdb*, you need to see an example. The procedure is easiest to show with a simple example, so I start with a rather contrived program that contains a typical bug.

The following is the contrived program, which I store in the file *dbgstest.c*:

```
#include <stdio.h>
static char buff[256];
void read_input(char *s);
int main(void)
{
    char *input = NULL; /* Just a pointer, no storage for string */
    read_input(input);
    /* Process command. */
    printf("You typed: %s\n", input);
    /* ... */
    return 0;
}
void read_input(char *s)
{
    printf("Command: ");
    gets(s);
}
```

This program's **main** function calls the **read\_input** function to get a line of input from the user. The **read\_input** function expects a character array in which it returns what the user types. In this example, however, **main** calls **read\_input** with an uninitialized pointer -- that's the bug in this simple program.

Build the program by using **gcc** with the **-g** option:

```
gcc -g -o dbgtest dbgtest.c
```

Ignore the warning message about the **gets** function being dangerous; I'm trying to use the shortcoming of that function to show how you can use **gdb** to track down errors.

To see the problem with this program, run it and type **test** at the Command: prompt:

```
./dbgtest
Command: test
Segmentation fault
```

The program dies after displaying the **Segmentation fault** message. For such a small program as this one, you can probably find the cause by examining the source code. In a real-world application, however, you may not immediately know what causes the error. That's when you have to use **gdb** to find the cause of the problem.

To use `gdb` to locate a bug, follow these steps:

- **Load the program under gdb.** To load a program named **dbgtest** in **gdb**, type the following:

  ```
  gdb dbgtest
  ```

- **Start executing the program under gdb by typing the run command. When the program prompts for input, type some input text.** The program fails as it did previously. Here's what happens with the **dbgtest** program:

  ```
  (gdb) run
  Starting program: /home/naba/rhls4e/dbgtest
  Command: test
  
  Program received signal SIGSEGV, Segmentation fault.
  0x00b6a4f6 in gets () from /lib/tls/libc.so.6
  (gdb)
  ```

- **Use the where command to determine where the program died.**

  For the `dbgst` program, this command yields this output:

  ```
  (gdb) where
  #0  0x00b644f6 in gets () from /lib/tls/libc.so.6
  #1  0x080483dc in read_input (s=0x0) at dbgst.c:22
  #2  0x0804839e in main () at dbgst.c:10
  (gdb)
  ```

  The output shows the sequence of function calls. Function call #0 — the most recent one — is to a C library function, `gets`. The `gets` call originates in the `read_input` function (at line 22 of the file `dbgst.c`), which in turn is called from the `main` function at line 10 of the `dbgst.c` file.

- **Use the list command to inspect the lines of suspect source code.**

  In `dbgst`, you may start with line 22 of `dbgst.c` file, as follows:

  ```
  (gdb) list dbgst.c:22
  17	)
  18	
  19	    void read_input(char *s)
  20	    {
  21		 printf("Command: ");
  22		 gets(s);
  23	    }
  24	}
  (gdb)
  ```

  After looking at this listing, you can tell that the problem may be the way `read_input` is called. Then you list the lines around line 10 in `dbgst.c` (where the `read_input` call originates):

  ```
  (gdb) list dbgst.c:10
  5	int main(void)
  6	{
  7	    char *input = NULL; /* Just a pointer, no storage for string */
  8	
  9	    read_input(input);
  10
  11	    /* Process command. */
  12	    printf("You typed: %s\n", input);
  13	}
  14	}
  (gdb)
  ```

  At this point, you can narrow the problem to the variable named `input`. That variable is an array, not a `NULL` (which means zero) pointer.

# Fixing bugs in gdb

Sometimes you can fix a bug directly in `gdb`. For the example program in the preceding section, you can try this fix immediately after the program dies
