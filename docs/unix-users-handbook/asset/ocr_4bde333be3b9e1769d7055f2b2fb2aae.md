| Parameter | Description |
| :--- | :--- |
| | the "$*" substitution (see Quoting below). |
| HISTFILE | If this parameter is set when the shell is invoked, its value is the path name of the file that is used to store the command history. The default value is $HOME/.sh_history. If the user has appropriate privileges and no HISTFILE is given, then no history file is used (see Command Re-entry below). |
| HISTSIZE | If this parameter is set when the shell is invoked, the number of previously entered commands accessible to this shell will be greater than or equal to this number. The default is 128. |
| HOME | The default argument (home directory) for the cd command. |
| MAIL | If this parameter is set to the name of a mail file and the MAILPATH parameter is not set, the shell informs the user of arrival of mail in the specified file. |
| MAILCHECK | This variable specifies how often (in seconds) the shell checks for changes in the modification time of any of the files specified by the MAILPATH or MAIL parameters. The default value is 600 seconds. When the time has elapsed the shell checks before issuing the next prompt. |
| MAILPATH | A list of file names separated by colons ( : ). If this parameter is set, the shell informs the user of any modifications to the specified files that have occurred within the last MAILCHECK seconds. Each file name can be followed by a ? and a message to be printed, in which case the message undergoes parameter and command substitution with the parameter $ _ defined as the name of the changed file. The default message is you have mail in $ _. |
| PATH | The search path for commands (see Execution below). The user cannot change PATH if executing rshx (except in the .profile file). |
| PS1 | The value of this parameter is expanded for parameter substitution, to define the primary prompt string which, by default, is $ followed by a space character. The character ! in the primary prompt string is replaced by the command number (see Command Re-entry below). To include a ! in the prompt, use !!. |
| PS2 | Secondary prompt string, by default > followed by a space character. |
| PS3 | Selection prompt string used within a select loop, by default #? followed by a space character. |
| PS4 | The value of this variable is expanded for parameter substitution and precedes each line of an execution trace. If PS4 is unset, the execution trace prompt is + followed by a space character. |
| SHELL | The path name of the shell is kept in the environment. When invoked, the shell is restricted if the value of this variable contains an r in the basename. |
| TMOUT | If set to a value greater than zero, the shell terminates if a command is not entered within the prescribed number of seconds after issuing the PS1 prompt. |
| VISUAL | Invokes the corresponding option when the value of this variable ends in emacs, gmacs, or vi (see set in Special Commands below). |

The shell gives default values to PATH, PS1, PS2, MAILCHECK, TMOUT,