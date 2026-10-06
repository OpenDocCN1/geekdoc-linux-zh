
# Command Summary 349

```
$ read line
Here is an entire      line \r
$ echo "$line"
Here is an entire      line r
$
```

Note in the final example that leading whitespace characters get “eaten” by the shell when read. You can change IFS if this poses a problem.

Also note backslash characters get interpreted by the shell when you read the line, and any that make it (double backslashes) will get through as a single backslash) get interpreted by echo if you display the value of variable.

- -A option to read says to not treat a character at the end of a line as line continuation.

# The readonly Command

General Format: `readonly vars`

This command tells the shell that the listed variables cannot be assigned values. These variables may be optionally assigned values on the readonly line. If you subsequently try to assign a value to a readonly variable, the shell issues an error message.

readonly are useful for ensuring that you don't accidentally overwrite the value of a variable. They’re also good for ensuring that other people using a shell program can't change the values of particular variables (for example, their HOME directory or their PATH). The readonly attribute is not passed down to subshells.

readonly with a -p option prints a list of your readonly variables.

Example

```
$ readonly DB=/users/steve/database
$DB=foo
sh: DB: is-readonly
$ echo $DB
/users/steve/database
```

- Assign value to DB and make it readonly
- Try to assign it a value
- Error message from the shell
- But can still access its value

# The return Command

General Format: `return n`

This command causes the shell to stop execution of the current function and immediately return to the caller with an exit status of n. If n is omitted, the exit status returned is that of the command executed immediately prior to the return.

# The set Command

General Format: `set options args`

This command is used to turn on or off options as specified by options. It is also used to set positional parameters, as specified by args.

Each single letter option in options is enabled if the option is preceded by a minus sign -, or disabled if preceded by a plus sign +. Options can be grouped, in

```
set fx
```

which enables the f and x options that can be selected.

Table A.9 summarizes the options that set

| Meaning | Option |
| --- | --- |
| | - | Don't treat subsequent args preceded by a - as options. If there are no arguments, the positional parameters are unset. |
| -a | Automatically export all variables that are subsequently defined or modified. |
| -b | If supported by the implementation, calls the shell to notify you when background jobs finish. |
| -C | Don't allow output redirection to overwrite files. > can still be used to force individual files to be overwritten even if this option is selected. |
| -e | Exit if any command that executes fails or has a nonzero exit status. |
| -f | Disable filename generation. |
| -h | Add commands inside functions to the hash list as they are defined, and not as they are executed. |
| -m | Turn on the job monitor. |
| -n | Read commands without executing them (useful for checking for balanced dots, and if fi). |
| +o | Write current option mode in command format. |
| -o m | Turn on option mode m (see Table A.10). |
| -u | Issue an error if a variable is referenced without having assigned a value or if a positional parameter is referenced without being set. |
| -v | Print each shell command line as it is read. |
| -x | Print each command and its arguments as it is executed, preceded by a +. |

Shell modes are turned on or off by using the -o and +o options, respectively, followed by an option name. These options are summarized in Table A.10.

# Table A.10 Shell Modes

| Mode | Meaning |
|---|---|
| allexport | Same as -a. |
| errexit | Same as -e. |
| ignoreeof | The exit command must be used to leave the shell. |
| monitor | Same as -m. |
| noclober | Same as -c. |
| noexec | Same as -n. |
| noglob | Same as -f. |
| nolog | Don't put function definitions in the history. |
| nounset | Same as -u. |
| verbose | Same as -v. |
| xtrace | The in-line editor is set to vi. |
| - | Same as -x. |

The command set -o without any options has the effect of listing all shell modes and their current settings. Each word listed in args is set to positional parameters $1, $2, ..., respectively. If the first word would start with a minus sign, it's safer to specify it with -- to avoid interpretation of that value. If args is supplied, the variable $# will be set to the number of parameters assigned after execution of the command.

# The shift Command

General Format: `shift`

This command causes the positional parameters $1, $2, ..., $n to be "shifted left" one place. That is, $2 is assigned to $1, $3, ..., and $n$ is adjusted accordingly. If format

```
shift n
```

Examples

- $ set a b c
$ echo "$name" "address" "phone"
$ shift

# The test Command

General Format: `test condition`

The shell evaluates condition and if the result of the evaluation is TRUE, returns a zero exit status. If the result of the evaluation is FALSE, a nonzero exit status is returned. If format `[ condition ]` is used, a space must appear immediately after [ and before ]. Remember that the parentheses are significant to the shell and must be quoted. Operators and operands (including parentheses) must be delimited by one or spaces so that test sees them as separate arguments. The -a operator has higher precedence than the -o operator. test is often used to test conditions in if, while, or until command.

# Examples

- see if per is executable

```
if test -x /etc/passwd
then
  ...
fi
```

- see if it's a directory or a normal file that's readable

```
if [ -d $file -o -f $file -a $file ]
then
  ...
```

# Table A.11 test Operators

| Operator | Returns TRUE (zero exit status) if |
| --- | --- |
| -b file | file is a block special. |
| -c file | file is a character special. |
| -d file | file is a directory. |
| -e file | file exists. |
| -f file | file is an ordinary file. |
| -g file | file has its group id (SGID) bit set. |
| -h file | file is a symbolic link. |
| -k file | file has its sticky bit set. |
| -L file | file is a symbolic link. |
| -p file | file is a named pipe. |
| -r file | file is readable by the process. |
| -S file | file is a socket. |
| -s file | file has nonzero length. |
| -t fd | fd is an open file descriptor associated with a terminal (1 is default). |
| -u file | file has its set user id (SUID) bit set. |
| -w file | file is writable by the process. |
| -x file | file is executable. |

# Appendix A Shell Summary

| Operator | Returns TRUE (zero exit status) if |
| --- | --- |
| String Operators | |
| string | string is not null. |
| -n string | string is not null (and must be seen by test). |
| -z string | string is null (and must be seen by test). |
| string = string | string is identical to string. |
| string != string | string is not identical to string. |
| Integer Comparison Operators | |
| int1 -eq int2 | int1 is equal to int2. |
| int1 -ge int2 | int1 is greater than or equal to int2. |
| int1 -gt int2 | int1 is greater than int2. |
| int1 -le int2 | int1 is less than or equal to int2. |
| int1 -lt int2 | int1 is less than int2. |
| int1 -ne int2 | int1 is not equal to int2. |
| Boolean Operators | |
| ! expr | expr is FALSE; otherwise, returns TRUE. |
| expr1 -a expr2 | expr1 is TRUE, and expr2 is TRUE. |
| expr1 -o expr2 | expr1 is TRUE, or expr2 is TRUE. |

# The times Command

General Format: `times`

Execution of this command causes the shell to write to standard output the total amount of time that has been used by the shell and all its child processes. For each, two numbers are listed: first the accumulated user time and then the accumulated system time.

Note that times does not report the time used by built-in commands.

Example

```
$ times
Print time used by processes
1m5 2m9s 1 min., 5 secs. user time, 2 mins., 9 secs. system time
8m22.23s 6m22.01s Used by child processes
$
```
