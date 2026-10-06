# Special Parameters

Table A.1 summarizes the special shell parameters.

| Table A.1 Special Parameter Variables |
| Parameter | Meaning |
| $# | The number of arguments passed to the program; or the number of parameters set by executing the set statement. |
| $* | Collectively references all the positional parameters as $1, $2, ... |
| $@ | Same as *, except when double-quoted("$@") collectively references all the positional parameters as "$1", "$2", ... |
| $0 | The name of the program being executed. |
| $$ | The process ID of the program being executed. |
| ! | The process status of the last command sent to the background for execution. |
| ? | The exit status of the last command not executed in the background. |
| $- | The current option flags in effect (see the set statement). |

In addition to these parameters, the shell has some other variables that it uses. Table A.2 summarizes the most important of these variables.

| Table A.2 Other Variables Used by the Shell |
| Variable | Meaning |
| CDPATH | The directories to be searched when cd is executed without a full path as argument. |
| ENV | The name of a file that the shell executes in the current environment when started interactively. |
| FCEDIT | The editor used by fc. If not, ed is used. |
| HISTFILE | If set, specifies a file to be used to store the command history. If not set or the file isn't writable, $HOME/.sh_history is used. |
| HISTSIZE | If set, specifies the number of previously entered commands accessible for editing. The default value is at least 128. |
| HOME | The user's home directory; the directory that cd changes to when no argument is supplied. |
| IFS | The internal field separator characters; used by the shell to delimit words when parsing the command line, for the read and set commands, when substituting the output from a back-quoted command, and when performing parameter substitution. Normally, it contains the three characters: space, horizontal tab, and newline. |