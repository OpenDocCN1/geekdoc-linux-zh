# Table 13.27 The shopt Command Options (continued)

| Option | Meaning |
|---|---|
| restricted_shell | The shell sets this option if it is started in restricted mode. The value may not be changed. This is not reset when the startup files are executed, allowing the startup files to discover whether or not a shell is restricted. |
| shift_verbose | If this is set, the shift built-in prints an error message when the shift count exceeds the number of positional parameters. |
| sourcepath | If set, the source built-in uses the value of PATH to find the directory containing the file supplied as an argument. Enabled by default. |
| source | A synonym for dot (.). |

# 13.20 Shell Built-In Commands

The shell has a number of commands that are built-in to its source code. Because the commands are built-in, the shell doesn't have to locate them on disk, making execution much faster. The help feature provided with bash gives you online help for any built-in command. The built-in commands are listed in Table 13.28.

# Table 13.28 Built-In Commands

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