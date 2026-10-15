
## Table 13.27 The shopt Command Options (continued)

| Option | Meaning |
|---|---|
| execfail | A noninteractive shell will not exit if it cannot execute the file specified as an argument to the exec built-in command. An interactive shell does not exit if exec fails. |
| expand_aliases | Aliases are expanded. Enabled by default. |
| extglob | The extended pattern-matching features (regular expression metacharacters derived from Korn shell for filename expansion) are enabled. |
| histappend | The history list is appended to the file named by the value of the HISTFILE variable when the shell exits, rather than overwriting the file. |
| histreedit | If readline is being used, a user is given the opportunity to re-edit a failed history substitution. |
| histverify | If set, and readline is being used, the results of history substitution are not immediately passed to the shell parser. Instead, the resulting line is loaded into the readline editing buffer, allowing further modification. |
| hostcomplete | If set, and readline is being used, bash will attempt to perform hostname completion when a word containing @ is being completed. Enabled by default. |
| huponexit | If set, bash will send SIGHUP (hangup signal) to all jobs when an interactive login shell exits. |
| interactive_comments | Allows a word beginning with # to cause that word and all remaining characters on that line to be ignored in an interactive shell. Enabled by default. |
| lithist | If enabled, and the cmdhist option is enabled, multiline commands are saved to the history with embedded newlines rather than using semicolon separators where possible. |
| mailwarn | If set, and a file that bash is checking for mail has been accessed since the last time it was checked, the message The mail in mailfile has been read is displayed. |
| nocaseglob | If set, bash matches filenames in a case-insensitive fashion when performing filename expansion. |
| nullglob | If set, bash allows filename patterns that match no files to expand to a null string, rather than themselves. |
| promptvars | If set, prompt strings undergo variable and parameter expansion after being expanded. Enabled by default. |
| restricted_shell | The shell sets this option if it is started in restricted mode. The value may not be changed. This is not reset when the startup files are executed, allowing the startup files to discover whether or not a shell is restricted. |
| shift_verbose | If this is set, the shift built-in prints an error message when the shift count exceeds the number of positional parameters. |
| sourcepath | If set, the source built-in uses the value of PATH to find the directory containing the file supplied as an argument. Enabled by default. |
| source | A synonym for dot (.). |

## 13.20 Shell Built-In Commands

The shell has a number of commands that are built-in to its source code. Because the commands are built-in, the shell doesn't have to locate them on disk, making execution much faster. The help feature provided with bash gives you online help for any built-in command. The built-in commands are listed in Table 13.28.

## Table 13.28 Built-In Commands

| Command | What It Does |
|---|---|
| : | Do-nothing command; returns exit status zero. |
| . | Executes program in context of current process; same as source. |
| . file | The dot command reads and executes command from file. |
| break | Breaks out of the innermost loop. |
| break [n] | See "The break Command" on page 919. |
| alias | Lists and creates "nicknames" for existing commands. |
| bg | Puts a job in the background. |
| bind | Display current key and function bindings, or binds keys to a readline function or macro. |
| builtin [sh-builtin [args]] | Runs a shell built-in, passing it args and returning zero exit status. Useful if a function and built-in have the same name. |
| cd [arg] | Changes the directory to home if no arg or to value of arg. |
