# Table 13.26 The Built-In set Command Options (continued)

| Name of Option | Shortcut Switch | What It Does |
|---|---|---|
| onecmd | -t | Exits after reading and executing one command. |
| physical | -P | If set, does not follow symbolic links when typing cd or pwd. The physical directory is used instead. |
| posix |  | Shell behavior is changed if the default operation doesn't match the POSIX standard. |
| privileged | -p | When set, the shell does not read the .profile or ENV file and shell functions are not inherited from the environment; automatically set for setuid scripts. |
| verbose | -v | Turns on the verbose mode for debugging. |
| vi |  | For command-line editing, uses the vi built-in editor. |
| xtrace | -x | Turns on the echo mode for debugging. |

# 13.19.2 The shopt Command and Options

The shopt (bash 2.x) command can also be used to turn shell options on and off.

# Table 13.27 The shopt Command Options

| Option | Meaning |
|---|---|
| cdable_vars | If an argument to the cd built-in command is not a directory, it is assumed to be the name of a variable whose value is the directory to change to. |
| cdspell | Corrects minor errors in the spelling of a directory name in a cd command. The errors checked for are transposed characters, a missing character, and a character too many. If a correction is found, the corrected path is printed, and the command proceeds. Only used by interactive shells. |
| checkhash | Bash checks that a command found in the hash table exists before trying to execute it. If a hashed command no longer exists, a normal path search is performed. |
| checkwinsize | Bash checks the window size after each command and, if necessary, updates the values of LINES and COLUMNS. |
| cmdhist | Bash attempts to save all lines of a multiple-line command in the same history entry. This allows easy re-editing of multiline commands. |
| dotglob | Bash includes filenames beginning with a dot (.) in the results of filename expansion. |