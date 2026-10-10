| This Function | Does the Following |
| :--- | :--- |
| fc -s [pat=rep] [cmd] | Re-executes the command after replacing the pattern pat with rep |
| fg [jobspec] | Puts the specified job in the foreground. If no job is specified, it puts the most recent job in the foreground. |
| getopts optstring name [args] | Gets optional parameters (which are called in shell scripts to extract arguments from the command line) |
| hash [-r] [name] | Remembers the full pathname of a specified command |
| help [cmd ...] | Displays help information for specified built-in commands |
| history [n] | Displays past commands or past n commands, if you specify a number n |
| jobs [-lnp] [ jobspec ... ] | Lists currently active jobs |
| kill [-s sigspec \|-SIGSPEC] [pid / jobspec] ... \| let arg [arg ...] | Evaluates each argument and returns 1 if the last arg is 0 |
| local [name=value] ... | Creates a local variable with the specified name and value (used in shell functions) |
| logout | Exits a login shell |
| popd [+/−n] | Removes entries from the directory stack |
| pushd [dir] | Adds a specified directory to the top of the directory stack |
| pwd | Prints the full pathname of the current working directory |
| read [−r] [name ...] | Reads a line from standard input and parses it |
| readonly [−f] [name ...] | Marks the specified variables as read-only so that the variables cannot be changed later |
| return [n] | Exits the shell function with the return value n |
| set [−abefhkmnptuvx1LCHP] [−o option] [arg ...] | Sets various flags |
| shift [n] | Makes the n+1 argument $1, the n+2 argument $2, and so on |
| source filename [arguments] | Reads and executes commands from a file |
| suspend [−f] | Stops execution until a SIGCONT signal is received |
| test expr | Evaluates the expression expr and returns zero if expr is true |

(continued)