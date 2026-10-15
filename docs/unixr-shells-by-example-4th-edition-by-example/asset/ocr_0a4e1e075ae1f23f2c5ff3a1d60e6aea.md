# Table 9.26 Special C/TC Shell Variablesᵃ ᵇ (continued)

| Variable | Meaning |
|---|---|
| autocorrect (+) | Invokes the spell checker before each attempt at filename, command, or variable completion. |
| autoexpand (+) | If set, the expand-history editor command is invoked automatically before each completion attempt. |
| autolist (+) | If set, possibilities are listed after an ambiguous completion. If set to ambiguous, possibilities are listed only when no new characters are added by completion. |
| autologout (+) | Its argument is the number of minutes of inactivity before automatic logout; the second optional argument is the number of minutes before automatic locking causes the screen to lock. |
| backslash_quote (+) | If set, a backslash will always quote itself, a single quote or a double quote. |
| cdpath | A list of directories in which cd should search for subdirectories if they aren't found in the current directory. |
| color (+) | Enables color display for the built-in command ls -f and passes --color=auto to ls. |
| complete (+) | If set to enhance, completion ignores case, considers periods, hyphens, and underscores to be word separators, and hyphens and underscores to be equivalent. |
| correct (+) | If set to cmd, commands are automatically spelling-corrected. If set to complete, commands are automatically completed. If set to all, the entire command line is corrected. |
| cwd | The full pathname of the current working directory. |
| dextract (+) | If set, pushd +n extracts the nth directory from the directory stack rather than rotating it to the top. |
| dirsfile (+) | The default location in which dirs -S and dirs -L look for a history file. If unset, ~/.cshdirs is used. |
| dirstack (+) | A list of all directories on the directory stack. |
| dunique (+) | Will not allow pushd to keep duplicate directory entries on the stack. |
| echo | If set, each command with its arguments is echoed just before it is executed. Set by the -x command-line option. |
| echo-style (+) | Sets the style for echo. If set to bsd will not echo a newline if the first argument is -n; if set to sysv, recognizes backlashed escape sequences in echo strings; if set to both, recognizes both the -n flag and backlashed escape sequences; the default, and if set to none, recognizes neither. |
| edit (+) | Sets the command-line editor for interactive shells; set by default. |