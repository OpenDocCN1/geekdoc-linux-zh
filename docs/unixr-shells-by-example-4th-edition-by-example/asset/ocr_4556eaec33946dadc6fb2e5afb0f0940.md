# Table 9.25 tcsh Built-In Commands and Their Meanings (continued)

| Command | Meaning |
|---|---|
| umask [ value ] | Displays the file creation mask. With value, sets the file creation mask. Value, given in octal, is XORed with the permissions of 666 for files and 777 for directories to arrive at the permissions for new files. Permissions cannot be added via umask. |
| unalias pattern | Removes all aliases whose names match pattern. unalias * thus removes all aliases. It is not an error for nothing to be unaliased. |
| uncomplete pattern | Removes all completions whose names match pattern. uncomplete * thus removes all completions. |
| unhash | Disables the internal hash table. |
| universe universe | Sets the universe to universe. (Masscomp/RTU only) |
| unlimit [-h] [resource] | Removes the limitation on resource or, if no resource is specified, all resource limitations. With -h, the corresponding hard limits are removed. Only the superuser may do this. |
| unsetenv pattern | Removes all environment variables whose names match pattern. unsetenv * thus removes all environment variables; this is a bad idea. If there is no pattern to be unsetenv, no error will result from this built-in. |
| unsetenv variable | Removes variable from the environment. Pattern matching, as with unset, is not performed. |
| @ [ var =expr ] | With no arguments, displays the values for all shell variables. With arguments, the variable var, or the nth word in the value of var, is set to the value that expr evaluates to. |
| @ [ var[n] =expr ] |  |
| ver [systype [command]] | Without arguments, prints SYSTYPE. With systype, sets SYSTYPE to systype. With systype and command, executes command under systype. systype may be bsd4.3 or sys5.3. (Domain/OS only) |
| wait | Waits for background jobs to finish (or for an interrupt) before prompting. |
| warp universe | Sets the universe to universe. (Convex/OS only) |
| watchlog | An alternate name for the log built-in command (q.v.). Available only if the shell was so compiled; see the version shell variable. |
| where command | Reports all known instances of command, including aliases, built-ins, and executables in path. |