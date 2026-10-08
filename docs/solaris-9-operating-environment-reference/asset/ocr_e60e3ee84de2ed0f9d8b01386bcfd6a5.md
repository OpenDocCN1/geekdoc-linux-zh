# csh 209

You can use the built-in continue command to terminate the execution of the current iteration of the loop, and the built-in command break to terminate execution of the foreach command. When this command is read from the terminal, the loop is read once, prompting with ? before any statements in the loop are executed.

glob wordlist

Perform file-name expansion on wordlist. Like echo, but no \ escapes are recognized. Words are delimited by NULL characters in the output.

goto label

The specified label is a file name and a command expanded to yield a line. The shell redirects its input as much as possible and searches for a line of form possibly preceded by space or Tab characters. Execution continues after the indicated line. It is an error to jump to a label that occurs between a while or for built-in command and its corresponding end.

hashstat

Print a statistics line indicating how effective the internal hash table for the path variable has been at locating commands (avoiding execs). Try an exec for each component of the path where the hash function indicates a possible hit and in each component that does not begin with /. These statistics reflect only the effectiveness of the path variable, the called variable.

history [-hr] [n]

+   - Display the history list; if n is given, display only the n most recent events.
-h Display the history list without leading numbers. Use this option to produce files suitable for sourcing, using the -h option to source.
-h Reverse the order of printout to be most recent instead of oldest first.

if (expr) command

The specified expression evaluates to true, execute the single command with arguments. Variable substitution on command happens early, at the same time it does for the rest of the if command. command must be a simple command, not a pipeline, a command list, or a parenthesized command list. Note: I/O redirection occurs even if expr is false when command is not executed (this is a bug).