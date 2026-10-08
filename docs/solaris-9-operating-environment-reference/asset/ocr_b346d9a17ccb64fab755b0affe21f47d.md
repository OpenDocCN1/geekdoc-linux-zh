# xargs

# 1561

-p

Prompt whether to execute command at each invocation. Turn on trace mode (-t) to write the command instance to be executed, followed by a prompt to standard error. An affirmative response (specific to the user's locale) read from /dev/tty executes the command; otherwise, skip that particular invocation of command.

-s size

Invoke command using many standard input arguments as possible and yielding a command-line length less than size(a positive decimal integer). Fewer arguments are used if:

+   - The total number of arguments exceeds that specified by the -n option.

+   - The total number of lines exceeds that specified by the -L option.

+   - End-of-file is encountered on standard input before size bytes accumulate.

Support values of size up to at least [LINE_MAX] bytes, provided that the specified constraints are met. You can give a value larger than that supported by the implementation or exceeding the specified constraints; xargs uses the largest value it supports within the constraints.

-t

Enable trace each generated command to standard error before invocation.

-x

Terminate if a command line containing number arguments (see the -n option) or number lines (see the -L option) do not fit in the implied or specified size(see the -s option value).

# Operands

command

The name of the command to be invoked, found by search path with the PATH environment variable; environ(5). If you omit command, the default is the echo(1) command. operand names any of the special built-in commands in shell_builtins(1), the results are undefined.

argument

An initial option or operand for the invocation of command.

# Usage

The 255 exit status enables a command to use xargs xargs to terminate if it knows that no further invocations using the current data stream will succeed. Thus, commandshould explicitly use with an appropriate value to avoid accidentally returning 255.

Input is parsed as lines; blank characters separate arguments. If xargs is used to bundle the output of commands like find -print or into commands to be executed, unexpected results are likely if files contain any blank characters or newline characters. You can fix this by using find to call a script that converts each file into a quoted string that is piped to xargs.

> Note — The quoting rules used by xargs are not the same as those in the shell. They were not consistent here because existing applications depend on the current rules and the shell syntax is not fully compatible