# TABLE 6.2 Continued

| Variable | Description |
| :--- | :--- |
| FUNNEST | Sets the maximum allowed function nesting level; when set to a number greater than 0 (if it is exceeded, the current command aborts) |
| GLOBIGNORE | A colon-separated list of patterns defining the set of filenames to be ignored by filename expansion |
| GROUPS | A variable array containing the list of groups of which the current user is a member |
| histchars | Up to three characters, which control history expansion |
| HISTCMD | The history number of the current command |
| HISTCONTROL | Controls which commands are entered in the shell history list |
| HISTFILE | The name of the file in which to save the shell history list (`.bash_history` by default) |
| HISTFILESIZE | The maximum number of lines to save in the history file |
| HISTIGNORE | A colon-separated list of patterns used to decide which commands are ignored for the history file |
| HISTSIZE | The maximum number of commands stored in the history list |
| HISTTIMEFORMAT | Used as a formatting string to print each command’s timestamp in Bash history, if set and not null |
| HOSTFILE | Contains the name of the file that should be read when the shell needs to complete a hostname |
| HOSTNAME | The name of the current host |
| HOSTTYPE | A string describing the machine the Bash shell is running on |
| IGNOREEOF | The number of consecutive EOF characters the shell must receive before exiting (if this value doesn’t exist, the default is 1) |
| INPUTRC | The name of the Readline initialization file (the default is `.inputrc`) |
| INSIDE_EMACS | Set only when process is running in an Emacs editor shell buffer and can disable line editing (disabling of line editing also depends on the value in the TERM variable) |
| LANG | The locale category for the shell |
| LC_ALL | Overrides the LANG variable, defining a locale category |
| LC_COLLATE | Sets the collation order used when sorting string values |
| LC_CTYPE | Determines the interpretation of characters used in filename expansion and pattern matching |
| LC_MESSAGES | Determines the locale setting used when interpreting double-quoted strings preceded by a dollar sign |
| LC_NUMERIC | Determines the locale setting used when formatting numbers |