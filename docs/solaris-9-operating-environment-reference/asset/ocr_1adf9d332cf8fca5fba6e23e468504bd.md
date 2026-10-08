# ksh, rksh 619

whence [-pv] name...

For each name, indicate how it would be interpreted if used as a command name. The -v option produces a more verbose report. The -p option does a path search for name even if name is an alias, a function, or a reserved word.

# Errors

Errors detected by the shell, such as syntax errors, return a non-zero exit status. Otherwise, the shell returns the exit status of the last command executed (see also the exit command). If the shell is used noninteractively, execution of the shell file is abandoned. Runtime errors detected by the shell are reported by printing the command or function name and the error condition. If the line number at which the error occurred is greater than 1, the line number is also printed in square brackets ([]) after the command or function name. For a noninteractive shell, an error condition encountered by a special built-in or other type of command writes a diagnostic message to standard error and as shown in the following table.

| Error | Built-in | Other Utilities |
|---|---|--|
| Shell language syntax error | Exit | Exit. |
| Utility syntax error (option or order error) | Exit | Do not exit. |
| Redirection error | Exit | Do not exit. |
| Variable assignment error | Exit | Do not exit. |
| Expansion error | Exit | Exit. |
| Command not found | N/A | May exit. |
| Dot script not found | Exit | N/A. |

An expansion error is one that occurs when the shell expansions are carried out (for example: $(xly): not a valid operator); an implementation can treat these syntax errors if it is able to detect them during tokenization instead of expansion.

If any of the errors shown as (may) exit occurs in a shell, the subshell (may) exit with a non-zero status, but the script containing the subshell does not exit because of error.

In all the cases shown in the table, an interactive shell writes a diagnostic message to standard error without exiting.

# Notes

Some very old shell scripts contain ^ as a synonym for the pipe character |. The built-in command : file reads the whole file before executing any commands. Therefore, alias and aliases commands in the file do not apply to any functions defined within the file.

When the shell executes a shell script that tries to execute a nonexistent command interpreter, the shell returns an erroneous diagnostic message that the shell file does not exist.