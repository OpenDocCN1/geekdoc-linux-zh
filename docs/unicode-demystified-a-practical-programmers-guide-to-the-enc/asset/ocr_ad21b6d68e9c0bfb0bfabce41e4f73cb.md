# Builtins

Builtins are commands that are part of (built into) the shell. When you give a simple filename as a command, the shell first checks whether it is a builtin. If it is, the shell executes it as part of the calling process; the shell does not fork a new process to execute the builtin. The shell does not need to search the directory structure for builtin programs because they are immediately available to the shell.

If the simple filename is not a builtin, the shell searches the directory structure for the program you want, using the PATH variable as a guide. When it finds the program, the shell forks a new process to execute the program.
Although they are not listed in Table 14-11, all the control structure keywords (if, foreach, endsw, and so on) are builtins. The table describes many of the tsh builtins, some of which are also built into other shells.

# Builtins || 14-11

| %job | A synonym for the fg builtin. The job is the number of the job you want to bring to the foreground (page 555). |
| %job & | A synonym for the bg builtin, where job is the number of the job you want to put in the background (page 556). |
| @ | Similar to the set builtin but evaluates numeric expressions. Refer to "Numeric Variables" on page 701. |
| alias | Creates and displays aliases. Refer to "Alias" on page 689. |
| alloc | Displays a report of the amount of free and used memory. |
| bg | Moves a suspended job into the background (page 556). |
| bindkey | Controls the mapping of keys to the tsh command line editor commands. Under zsh bindkey works similarly. The most common-uses follow. |
| | Without any arguments, bindkey lists all key bindings. |
| bindkey -l | Lists all the available editor commands and gives a short description of each. |
| bindkey -e | Causes the editor to use GNU emacs-like key bindings. |
| bindkey -v | Causes the editor to use vi-like key bindings.|