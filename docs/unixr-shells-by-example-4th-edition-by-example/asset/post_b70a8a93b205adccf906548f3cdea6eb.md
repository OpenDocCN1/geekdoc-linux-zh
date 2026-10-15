
## Table 10.11 C and TC Shell Built-In Commands and Their Meanings (continued)

| Command | Meaning |
|---|---|
| nice [+n|-n] [command] | Increments the process priority value for the shell or command by n. The higher the priority value, the lower the priority of a process and the slower it runs. If command is omitted, nice increments the value for the current shell. If no increment is specified, nice sets the nice value to 4. The range of nice values is from -20 through 19. Values of n outside this range set the value to the lower or higher boundary, respectively. +n Increments the process priority value by n. -n Decrements by n. This argument can be used only by the superuser. |
| nohup [command] | Runs command with HUPs (hangups) ignored. With no arguments, ignores HUPs throughout the remainder of a script. |
| notify [%]job | Notifies the user asynchronously when the status of the current or of a specified job changes. |
| onintr [- | label] | Controls the action of the shell on interrupts. With no arguments, onintr restores the default action of the shell on interrupts. (The shell terminates shell scripts and returns to the terminal command input level.) With the minus sign argument, the shell ignores all interrupts. With a label argument, the shell executes a goto label when an interrupt is received or a child process terminates because it was interrupted. |
| popd [+n] | Pops the directory stack and cd to the new top directory. The elements of the directory stack are numbered from zero, starting at the top. +n Discard the nth entry in the stack. |
| pushd [+n | dir] | Pushes a directory onto the directory stack. With no arguments, exchange the top two elements. +n Rotates the nth entry to the top of the stack and cd to it. dir Pushes the current working directory onto the stack and change to dir. |
| rehash | Recomputes the internal hash table of the contents of directories listed in the path variable to account for new commands added. |
| repeat count command | Repeat command count times. |
| set [var [= value]] | See "Variables" on page 440. |
| setenv [VAR [word]] | See "Variables" on page 440. The most commonly used environment variables, USER, TERM, and PATH, are automatically imported to and exported from the csh variables, user, term, and path; there is no need to use setenv for these. In addition, the shell sets the PATH environment variable from the csh variable cwd whenever the latter changes. |
| shift [variable] | The components of argv, or variable, if supplied, are shifted to the left, discarding the first component. It is an error for variable not to be set, or to have a null value. |
| source [-h] name | Reads commands from name. Source commands may be nested, but if they are nested too deeply, the shell may run out of file descriptors. An error in a sourced file at any level terminates all nested source commands. Used commonly to re-execute the .login or .cshrc files to ensure variable settings are handled within the current shell, that is, to make sure the shell does not create (fork) a child shell. -h Places commands from the filename on the history list without executing them. |
| stop [%job] ... | Stops the current or specified background job |
| suspend | Stops the shell in its tracks, much as if it had been sent a stop signal with ^Z. This is most often used to stop shells started by su. |
| switch (string) | See "The switch Command" on page 557. |
| time [command] | With no argument, print a summary of time used by this shell and its children. With an optional command, execute command and print a summary of the time it uses. |
| umask [value] | Displays the file creation mask. With value, sets the file creation mask. Value, given in octal, is XORed with the permissions of 666 for files and 777 for directories to arrive at the permissions for new files. Permissions cannot be added via umask. |
| unalias pattern | Discards aliases that match (filename substitution) pattern. All aliases are removed by unalias *. |
| unhash | Disables the internal hash table. |
| unlimit [-h] [resource] | Removes a limitation on resource. If no resource is specified, all resource limitations are removed. See the description of the limit command for the list of resource names. -h Removes corresponding hard limits. Only the superuser may do this. |
| unset pattern | Removes variables whose names match (filename substitution) pattern. All variables are removed by unset *; this has noticeably distasteful side effects. |
| unsetenv variable | Removes variable from the environment. Pattern matching, as with unset, is not performed. |
| wait | Waits for background jobs to finish (or for an interrupt) before prompting. |
| while (expr) | See "The while Loop" on page 564. |
