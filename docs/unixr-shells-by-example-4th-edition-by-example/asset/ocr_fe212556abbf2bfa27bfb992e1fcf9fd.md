# Table 14.11 The shopt Command Options (continued)

| Option | Meaning |
|---|---|
| sourcepath | If set, the source built-in uses the value of PATH to find the directory containing the file supplied as an argument. Enabled by default. |
| source | A synonym for dot (.). |

# 14.12 Shell Built-In Commands

The shell has a number of commands that are built into its source code. Because the commands are built-in, the shell doesn't have to locate them on disk, making execution much faster. The help feature provided with bash gives you online help for any built-in command. The built-in commands are listed in Table 14.12.

# Table 14.12 Built-In Commands

| Command | What It Does |
|---|---|
| . | Executes program in context of current process; same as source. |
| . file | The dot command reads and executes command from file. |
| : | Do-nothing command; returns 0 exit status. |
| alias | Lists and creates "nicknames" for existing commands. |
| bg | Puts a job in the background. |
| bind | Displays current key and function bindings, or binds keys to a readline function or macro.ᵃ |
| break | Breaks out of the innermost loop. |
| break [n] | See "The break Command" on page 919. |
| builtin [sh-builtin [args]] | Runs a shell built-in, passing it args, and returning 0 exit status. Useful if a function and built-in have the same name.ᵃ |
| cd [arg] | Changes the directory to home if no arg or to value of arg. |
| command command [arg] | Runs a command even if a function has the same name (i.e., bypasses function lookup).ᵃ |
| continue [n] | See "The continue Command" on page 920. |
| declare [var] | Displays all variables or declares variables with optional attributes.ᵃ |
| dirs | Displays a list of currently remembered directories resulting from pushd. |