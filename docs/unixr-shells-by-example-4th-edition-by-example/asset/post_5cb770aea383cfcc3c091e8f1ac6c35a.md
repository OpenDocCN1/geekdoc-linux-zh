
## Table 9.25 tcsh Built-In Commands and Their Meanings (continued)

| Command | Meaning |
|---|---|
| setspath LOCAL|site|cpu ... | Sets the system execution path. |
| settc cap value | Tells the shell to believe that the terminal capability cap (as defined in termcap(5)) has the value value. No sanity checking is done. Concept terminal users may have to settc xn no to get proper wrapping at the rightmost column. |
| setty [-d|-q|-x] [-a] [+|-]mode | Controls which tty modes the shell does not allow to change. -d, -q, or -x tells setty to act on the edit, quote, or execute set of tty modes, respectively; without -d, -q, or -x, execute is used. Without other arguments, setty lists the modes in the chosen set that are fixed on (+mode) or off (-mode). The available modes, and thus the display, vary from system to system. With -a, lists all tty modes in the chosen set whether or not they are fixed. With +mode, -mode, or mode, fixes mode on or off or removes control from mode in the chosen set. For example, setty +echo echok fixes echo mode on and allows commands to turn echoe mode on or off, both when the shell is executing commands. |
| setxvers [string] | Sets the experimental version prefix to string, or removes it if string is omitted. |
| shift [ variable ] | The components of argv, or variable, if supplied, are shifted to the left, discarding the first component. It is an error for variable not to be set, or to have a null value. |
| source [-h ] name | Reads commands from name. Source commands may be nested, but if they are nested too deeply, the shell may run out of file descriptors. An error in a sourced file at any level terminates all nested source commands. Commonly used to re-execute the .login or .cshrc files to ensure variable settings are handled within the current shell, i.e., shell does not create a child shell (fork). With -h, places commands from the filename on the history list without executing them. |
| stop [%job] ... | Stops the current or specified background job. |
| suspend | Stops the shell in its tracks, much as if it had been sent a stop signal with ^Z. This is most often used to stop shells started by su. |
| switch (string) | See "The switch Command" on page 557. |
| telltc | Lists the values of all terminal capabilities (see termcap(5)). |
| time [ command ] | With no argument, prints a summary of time used by this shell and its children. With an optional command, executes command and prints a summary of the time it uses. |
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
