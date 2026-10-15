# Table 14.12 Built-In Commands (continued)

| Command | What It Does |
|---|---|
| disown | Removes an active job from the job table. |
| echo [args] | Displays args terminated with a newline. |
| enable | Enables and disables shell built-in commands.ᵃ |
| eval [args] | Reads args as input to the shell and executes the resulting command(s). |
| exec command | Runs command in place of this shell. |
| exit [n] | Exits the shell with status n. |
| export [var] | Makes var known to subshells. |
| fc | History's fix command for editing history commands. |
| fg | Puts background job into foreground. |
| getopts | Parses and processes command-line options. |
| hash | Controls the internal hash table for quicker searches for commands. |
| help [command] | Displays helpful info about built-in commands and, if command is specified, detailed help about that built-in command.ᵃ |
| history | Displays the history list with line numbers. |
| jobs | Lists jobs put in the background. |
| kill [-signal process] | Sends the signal to the PID number or job number of the process. Type kill -l for a list of signals. |
| let | Used for evaluating arithmetic expressions and assigning results of arithmetic calculations to variables. |
| local | Used in functions to restrict the scope of variables to the function. |
| logout | Exits the login shell. |
| popd | Removes entries from the directory stack. |
| pushd | Adds entries to the directory stack. |
| pwd | Prints present working directory. |
| read [var] | Reads line from standard input into variable var. |
| readonly [var] | Makes variable var read-only. Cannot be reset. |
| return [n] | Returns from a function where n is the exit value given to the return. |