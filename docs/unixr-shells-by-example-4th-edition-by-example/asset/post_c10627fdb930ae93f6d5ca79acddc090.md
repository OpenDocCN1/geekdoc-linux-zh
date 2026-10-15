
### Table 9.25 tcsh Built-In Commands and Their Meanings (continued)

| Command | Meaning |
|---|---|
| which command | Displays the command that will be executed by the shell after substitutions, path searching, etc. The built-in command is just like which(1), but it correctly reports tcsh aliases and built-ins and is 10 to 100 times faster. |
| while (expr) | See "Looping Control Commands" on page 566. |

## 9.20.1 Special Built-In C/TC Shell Variables

The built-in shell variables have special meaning to the shell and are used to modify and control the way many of the shell commands behave. They are local variables and therefore most of them are set in the .tcshrc file for the TC shell, and the .cshrc file for the C shell if they are to be passed on to and affect child C/TC shells.

When the shell starts up, it automatically sets the following variables: addsuffix, argv, autologout, command, echo_style, edit, gid, group, home, logname, oid, path, prompt, prompt2, prompt3, shell, shlvl, tcsh, term, tty, uid, user, and version. Unless the user decides to change them, these variables will remain fixed. The shell also keeps track of and changes special variables that may need periodic updates, such as cwd, dirstack, owd, and status, and when the user logs out, the shell sets the logout variable.

Some of the local variables have a corresponding environment variable of the same name. If one of the environment or local variables is affected by a change in the user's environment, the shell will synchronize the local and environment variables* so that their values always match. Examples of cross-matched variables are afsuser, group, home, path, shlvl, term, and user. (Although cwd and PWD have the same meaning, they are not cross-matched. Even though the syntax is different for the path and PATH variables, they are automatically cross-matched if either one is changed.)

### Table 9.26 Special C/TC Shell Variables a b

| Variable | Meaning |
|---|---|
| addsuffix (+) | For filename completion, adds slashes at the end of directories and space to the end of normal files if they are matched. Set by default. |
| afsuser (+) | If set, autologout's autolock feature uses its value instead of the local username for Kerberos authentication. |
| ampm (+) | If set, all times are shown in 12-hour AM/PM format. |
| argv | An array of command-line arguments to the shell; also represented as $1, $2, and so on. |
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
| echo-style (+) | Sets the style for echo. If set to bsd will not echo a newline if the first argument is -n; if set to sysv, recognizes backslash escape sequences; if set to both, recognizes both the -n flag and backslash escape sequences; the default, and if set to none, recognizes neither. |
| edit (+) | Sets the command-line editor for interactive shells; set by default. |

> 9. This is true unless the variable is a read-only variable, and then there will be no synchronization.
