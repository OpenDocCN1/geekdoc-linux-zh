| This Function | Does the Following |
|---|---|
| fc -s [pat=rep] [cmd] | Re-executes the command after replacing the pattern pat with rep. |
| fg [jobspec] | Puts the specified job in the foreground. If no job is specified, it puts the most recent job in the foreground. |
| getopts optstring name [args] | Gets optional parameters (which are called in shell scripts to extract arguments from the command line). |
| hash [-r] [name] | Remembers the full pathname of a specified command. |
| help [cmd ...] | Displays help information for specified built-in commands. |
| history [n] | Displays past commands or past n commands, if you specify a number n. |
| jobs [-lnp] [ jobspec ... ] | Lists currently active jobs. |
| kill [-s sigspec | -sigspec] [pid / jobspec] ... | Evaluates each argument and returns 1 if the last arg is 0. |
| let arg [arg ...] | Creates a local variable with the specified name and value (used in shell functions). |
| local [name=value] ... | Exits a login shell. |
| logout | Removes entries from the directory stack. |
| popd [+/-n] | Adds a specified directory to the top of the directory stack. |
| pushd [dir] | Prints the full pathname of the current working directory. |
| pwd | Reads a line from standard input and parses it. |
| read [-r] [name ...] | Marks the specified variables as read-only, so that the variables cannot be changed later. |
| readonly [-f] [name ...] | Exits the shell function with the return value n. |
| return [n] | Sets various flags. |
| set [-abefhkmnptuvx] [ -o option] [arg ...] | Makes the n+1 argument $1, the n+2 argument $2, and so on. |
| shift [n] | Reads and executes commands from a file. |
| source filename [arguments] | Stops execution until a SIGCONT signal is received. |
| suspend [-f] | Evaluates the expression expr and returns zero if expr is true. |
| test expr | Prints the accumulated user and system times for processes run from the shell. |
| times |  |