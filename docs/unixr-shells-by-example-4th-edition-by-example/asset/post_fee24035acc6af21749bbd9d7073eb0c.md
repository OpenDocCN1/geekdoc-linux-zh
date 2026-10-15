
The shell in which a variable is created is called the parent shell. If a new shell is started from the parent shell, it is called the child shell. Some of the environment variables, such as HOME, LOGNAME, PATH, and SHELL, are set before you log in by the /bin/login program. Normally, environment variables are set in the .profile file in the user's home directory.

## Setting Environment Variables.

To set environment variables, the export command is used either after assigning a value or when the variable is set. All variables in a script can be exported by turning on the allexport option to the set command (e.g., set -o allexport).

### EXAMPLE 11.37

```
1  $ TERM=wyse ; export TERM
2  $ export NAME ="John Smith"
   $ print $NAME
   John Smith
3  $ print $$ 
   319
4  $ ksh
5  $ print $$
   340
6  $ print $NAME
   John Smith
7  $ NAME="April Jenner"
   $ print $NAME
   April Jenner
8  $ exit
9  $ print $$
   319
10 $ print $NAME
    John Smith
```

### EXPLANATION

- 1 The TERM variable is assigned wyse. The variable is exported. Now processes started from this shell will inherit the variable.
- 2 The variable is exported and defined in the same step. (New with the Korn shell.)
- 3 The value of this shell's PID is printed.
- 4 A new Korn shell is started. The new shell is the child, the original shell is its parent.
- 5 The PID of the new Korn shell, stored in the $$ (340) variable, is printed.
- 6 The variable was exported to the new shell and is displayed.
- 7 The variable is reset to April Jenner and displayed.
- 8 This Korn child shell is exited. The parent shell will return.
- 9 The PID of the parent, 319, is displayed again.
- 10 The variable NAME contains its original value. Variables retain their values when exported from parent to child. The child cannot change the value of a variable for its parent.

## Special Environment Variables.

The Korn shell assigns default values to the environment variables, PATH, PS1, PS2, PS3, PS4, MAILCHECK, FCEDIT, TMOUT, and IFS. The SHELL, LOGNAME, USER, and HOME are set by the /bin/login program. You can change the values of the defaults and set the others listed in Table 11.9.

### Table 11.9 Korn Shell Environment Variables

| Variable Name | Meaning |
|---|---|
| _ (underscore) | The last argument of the previous command. |
| CDPATH | The search path for the cd command. A colon-separated list of directories used to find a directory if the /, ./ or ../ is not at the beginning of the pathname. |
| COLUMNS | If set, defines the width of the edit window for shell edit modes and the select command. |
| EDITOR | Pathname for a built-in editor: emacs, gmacs, or vi. |
| ENV | A variable set to the name of a file, containing functions and aliases, that the Korn shell will invoke when the ksh program is invoked. On versions newer than 1988, this file is only executed when ksh is invoked interactively, not for noninteractive shells. The variable is not expanded if the privileged option is turned on. |
| ERRNO | System error number. Its value is the error number of the most recently failed system call. |
| FCEDIT | Default editor name for the fc command. On versions newer than 1988, this variable is called HISTEDIT, and the fc command is hist. |
| FPATH | A colon-separated list of directories that defines the search path for directories containing auto-loaded functions. |
| HISTEDIT | For versions of the Korn shell newer than 1988, the new name for FCEDIT. |
| HISTFILE | Specifies file in which to store command history. |
| HISTSIZE | Maximum number of commands from the history that can be accessed; default is 128. |
| HOME | Home directory; used by cd when no directory is specified. |
| IFS | Internal field separators, normally space, tab, and newline, used for field splitting of words resulting from command substitution, lists in loop constructs, and reading input. |
| LINENO | Current line number in script. |
| LINES | Used in select loops for vertically displaying menu items; default is 24. |
