TABLE 18.1: BOURNE SHELL BUILT-INS
| Built-In | Description |
| :--- | :--- |
| `alias (unalias)` | Creates or removes a pseudonym or shorthand for a command or series of commands. |
| `bg` | Background; controls process execution. |
| `break` | Used to exit from a `for` or enclosing `while` loop, if one is executing. If you specify `n` (a number), then that many levels of looping is terminated. |
| `case` | Allows user a choice from a list of actions by evaluating a series of true and false statements. The first true response is executed, ending the case statement. |
| `cd` | Changes the working directory. |
| `chdir` | Same as `cd`. |
| `continue` | Allows escape from or advance within an enclosing `while`, `for`, `foreach`, or `until` loop. |
| `echo` | Causes arguments to be separated by blanks and terminated by a newline to standard output. |
| `eval` | Allows arguments to the `eval` command to be read as input to the shell and executes the resulting commands. |
| `exec` | Specified by arguments; executes in place of the shell without creating a new process. Input/output arguments may appear and, if no other arguments are given, cause the shell input/output to be modified. |
| `exit` | Causes the calling shell or shell script to exit. |
| `export` | Sends the variable and its value to the shell environment, causing its value to be set and used by all other commands until the `unset` command is used. |
| `[..]` | When used in a loop or as a control, it is a shortcut for the `test` built-in. |
| `[...]` | When used in file access, it can be used to match one of a set (abc) or a range (a-c) of characters. (i.e., `\'ls [cbj]at\'`, which would find `cat` and `bat` but not `nat`). |
| `fg` | Foreground; controls process execution. Also brings a job to the foreground. |
| `for` | Repeatedly executes an action a specified number of times. |
| `getopts` | Retrieves options and option arguments from a list of parameters. |
| `hash` | Recalculates the internal hash table of the contents of the directories listed in the path environmental variable to account for new commands added. |