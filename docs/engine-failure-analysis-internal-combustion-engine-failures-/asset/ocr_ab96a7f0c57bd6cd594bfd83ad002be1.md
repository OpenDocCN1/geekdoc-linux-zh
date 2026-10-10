functions. Note that you must insert a space before and after each curly brace, and you must end the command list with a semicolon.

# SHELL FUNCTION SYNTAX

| Command Form | Meaning |
|---|---|
| `[ function ] name { command1; command2; ... ;}` | Create a function called *name* that includes the specified commands. |
| `name () { command1; command2; ... ;}` | Create a function called *name* that includes the specified commands. |

# EXAMPLES

| This Command | Does the Following |
|---|---|
| `list () { ls -Sh | less; }` | Creates a shell function called *list* that executes the `ls` command and pipes its output to `less`. |
| `detar () { gunzip *doc.tar.gz ; tar -xvf *.doc.tar }` | Creates a shell function that unzips all the `*.doc.tar.gz` files and extracts the files from the decompressed `*.doc.tar` archives. |

# Job Control

Normally, processes execute in the *foreground*, which means that they take over the current shell session while running. If you begin an especially time-consuming process, such as compiling a lengthy program, you may wish to place a job in the *background*. By doing this, you regain control of the shell session, and the process executes