# Advanced Bash–Scripting Guide

```
bash$ echo -l /usr/share/apps/kjezr/sounds'
total 40 -rw-r--r-- 1 root root 716 Nov 7 2000 reflect.au -rw-r--r-- 1 root 362 Nov 7
```

This command is a shell builtin, and not the same as
bin/echo, although its behavior is similar.

```
bash$ type -a echo
echo is a shell builtin
echo is /bin/echo
```

printf
printf, formatted print, command is an enhanced echo. It is a limited variant of the C language
printf, and the syntax is somewhat different.

printf format-string... parameter...

This is the Bash builtin version of the /bin/printf or /usr/bin/printf command. See the
printf manpage (of the system command) for in-depth coverage.

> Older versions of Bash may not support printf.

# Example 11-1. printf in action

```
#!bin/bash
# printf demo

PI=3.14159265358979
DecimalConstant=31733
Message1="Greetings,"
Message2="Earthling."

echo
printf "Pi to 2 decimal places = %1.2f" $PI
echo
printf "Pi to 9 decimal places = %1.9f" $PI  # It even rounds off correctly.

printf "\n"
  # Prints a line feed,
  # equivalent to 'echo'

printf "Constant = \t%d\n" $DecimalConstant  # Inserts tab (t)

printf "%% %s \n" $Message1 $Message2
echo

------------------------------------
# Simulation of C function, 'sprintf'.
# Loading a variable with a formatted string.
```

Chapter 11. Internal Commands and Builtins 123