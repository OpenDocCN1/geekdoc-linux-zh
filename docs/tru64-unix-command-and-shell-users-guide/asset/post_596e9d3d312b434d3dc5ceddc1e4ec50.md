
# Export global variables
export PATH ENV EDITOR FCEDIT PS1

# Set mail variables
MAIL=/usr/spool/mail/$LOGNAME
MAILCHECK=300

## Table 8-12: Example Korn or POSIX Shell .profile Script

| Command | Description |
|---|---|
| Set Environment Variables | |
| PATH=/usr/bin:/usr/local/bin | Specifies the search path. In this case, /usr/bin is searched first and /usr/local/bin is searched second. |
| ENV=$HOME/.kshrc | Specifies $HOME/.kshrc as the login script. |
| EDITOR=vi | Specifies vi as the default editor for command line editing at the shell prompt and for file name completion. |
| FCEDIT=vi | Specifies vi as the default editor for the fc command. |
| PS1="'hostname' [!] $ " | The PS1 variable specifies the Korn or POSIX shell prompt. Its default value is $. This variable assignment specifies that your prompt should be changed to the following: the output of the hostname command, followed by the command number of the current command, followed by the dollar sign ($). For example, if the name of your system is boston, and the current command is numbered 30, your prompt would be the following: boston[30] $. |
| Export Global Variables | |
| export PATH ENV EDITOR FCEDIT PS1 | Specifies that the values of the PATH, ENV, EDITOR, FCEDIT, and PS1 variables should be exported to all subshells. |
| Set Mail Variables | |
| MAIL=/usr/spool/mail/$LOGNAME | Specifies the pathname of the file used by the mail system to detect the arrival of new mail. In this case, the mail system would look in your user name subdirectory under the /usr/spool/mail directory. |
| MAILCHECK=300 | Specifies that the shell should check for mail every 300 seconds (5 minutes). |
| a For information on the fc command, see Section 8.4.4. |

In the following .kshrc login script, shell variables, command aliases, and command history variables are set, as well as the permissions for file creation. Table 8–13 explains each part of the script.

```
# Set shell variables
set -o monitor
set -o trackall

# Set command aliases
alias rm='rm -i '
alias rename='mv '
alias l 'ls -l'
alias c clear

# Set history variables
HISTSIZE=40

# Set file creation permissions
umask 027
```

## Table 8–13: Example .kshrc Script

| Command | Description |
|---|---|
| Shell Variables | |
| set -o monitor | Specifies that the shell should monitor all background processes and display a completion message when the process finishes. |
| set -o trackall | Specifies that the shell should track all commands that you execute. Once a command is tracked, the shell stores the location of the command and finds the command more quickly the next time you enter it. |
| Command Aliases | |
| alias rm='rm -i' | Specifies the use of the -i option (which prompts you for file deletion) with the rm command. |
| alias rename='mv' | Specifies rename as a new name for the mv command. |
| alias l='ls -l' | Defines a short name for the ls -l command that lists directory files in the long format. |
| alias c='clear' | Defines a short name for the clear command that clears your screen. |
| History Variables | |
| HISTSIZE=40 | Instructs the shell to store the last 40 commands in the history buffer. |

**Table 8–13: Example .kshrc Script (cont.)**

| Command | Description |
|---|---|
| Set File Creation Permissions | |
| `umask 027` | Specifies the maximum permissions for all new files created. This command provides all permissions for the owner, read, and execute permissions for members of the same group, and no permissions for all others. The umask is not inherited by subshells. |

## 8.4.2 Metacharacters

Table 8–14 describes Korn or POSIX shell metacharacters (characters that have special meaning to the shell). The meaning of these meta characters are grouped by interpretation when they appear in a shell script, in a Filename specification, when used to quote other characters, in an Input/Output specification, or when used to indicate variable substitution.

**Table 8–14: Korn or POSIX Shell Metacharacters**

| Metacharacter | Description |
|---|---|
| Syntactic | |
| `|` | Separates commands that are part of a pipeline. |
| `&&` | Runs the next command if the current command succeeds. |
| `||` | Runs the next command if the current command fails. |
| `;` | Separates commands that should be executed sequentially. |
| `;;` | Separates elements of a case construct. |
| `&` | Runs commands in the background. |
| `()` | Groups commands in a subshell as a separate process. |
| `{}` | Groups commands without creating a subshell. |
| File Name | |
| `/` | Separates the parts of a file’s pathname. |
| `?` | Matches any single character except a leading dot (`.`). |
| `*` | Matches any character sequence except a leading dot (`.`). |
