Read the complete file, then execute the commands in the current shell environment. Use the search path specified by PATH to find the directory containing file. If you specify any arguments, they become the positional parameters. Otherwise, leave the positional parameters unchanged. The exit status is the status of the last command executed: the loop termination test.

# Else Also

+   alias(1), break(1), cd(1), chmod(1), csh(1), echo(1), exec(1), exit(1),
find(1), getopctvt(1), getopts(1), glob(1), hash(1), history(1),
intro(1), jobs(1), kill(1), ksh(1), let(1), limit(1), login(1),
logout(1), ncan(1), newgrp(1), nohup(1), print(1), pwd(1), read(1),
readonly(1), set(1), sh(1), shift(1), suspend(1), time(1), times(1),
trap(1), typeset(1), umask(1), wait(1), test(1B), chdir(2), chmod(2),
creat(2), umask(2), getopt(3C), profile(4), environ(5)

# shift — Shell Built-in Function to Traverse Either a Shell's
Argument List or a List of Field-Separated Words

# Synopsis

+   sh
shift [n]

+   csh
shift [variable]

+   ksh
shift [n]

# Description

The command is a shell built-in that traverses the argument list
of the shell or a list of field-separated words.

# Bourne Shell

The positional parameters from $n=1... are renamed $1.... The default n is 1.

# C Shell

The components of argv, or variable, if supplied, are shifted to the left, discarding
t first component. It is an error for a variable not to be set or to have a null value.

# Korn Shell

The positional parameters from $n+1 $n+1... are renamed $1.... The default n is 1.
The parameter n can be any arithmetic expression that evaluates to a nonnegative
number less than or equal to $.

ksh(1) commands that are preceded by one or two asterisks (*) are treated specially

in the following ways.