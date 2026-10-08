| Command | Execution |
|---|---|
| ENTER | Execute a command line. |
| ; | Separate commands on the same command line. |
| command\\opts args | Enter backslash before carriage return to continue entering a command on the next line. |
| ' command ' | Execute a command. |
| $( command ) | Execute a command. |
| **Special Characters for Filename Expansion** | **Execution** |
| \* | Match on any set of characters. |
| ? | Match on any single characters. |
| [ ] | Match on a class of possible characters. |
| \\ | Quote the following character. Used to quote special characters. |
| **Redirection** | **Execution** |
| command > filename | Redirect the standard output to a file or device, creating the file if it does not exist and overwriting the file if it does exist. |
| command < filename | Redirect the standard input from a file or device to a program. |
| command >> filename | Redirect the standard output to a file or device, appending the output to the end of the file. |
| command > ! filename | In the C shell and the Korn shell, the exclamation point forces the overwriting of a file if it already exists. This overrides the **noclobber** option. |
| command 2> filename | Redirect the standard error to a file or device in the Bourne shell. |
| command 2>> filename | Redirect and append the standard error to a file or device in the Bourne shell. |
| command 2>&1 | Redirect the standard error to the standard output in the Bourne shell. |
| command >& filename | Redirect the standard error to a file or device in the C shell. |
| **Pipes** | **Execution** |
| command | command | Pipe the standard output of one command as input for another command. |
| command | & command | Pipe the standard error as input for another command in the C shell. |

TABLE 8-6  The Shell Operations