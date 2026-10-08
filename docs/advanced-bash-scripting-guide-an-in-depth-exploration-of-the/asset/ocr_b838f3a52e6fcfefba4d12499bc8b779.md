# Advanced Bash-Scripting Guide

```
# Let's try something else.
echo
echo "A line of text containing
a linefeed."
# Prints as two distinct lines (embedded linefeed).
# But, is the "$" variable prefix really necessary?
echo
echo "This string splits
on two lines."
# No, the "$" is not needed.
echo
echo "------------------"
echo
echo -n "Another line of text containing
a linefeed."
# Prints as two distinct lines (embedded linefeed).
# Even the -n option fails to suppress the linefeed.
```

echo
echo
echo "------------------"
echo
echo

# However, the following doesn't work as expected.
# Why not? Hint: Assignment to a variable.
string1=$Yet another line of text containing
a linefeed (maybe).

echo $string1
# Another line of text containing a linefeed (maybe).
# Linefeed becomes a space.

# Thanks, Steve Parker, for pointing this out.

> This command is a shell builtin, and not the same as /bin/echo, although itsnbehavior is similar.

```
bash$ type -a echo
echo is a shell builtin
echo is /bin/echo
```

# printf

The printf, formatted print, command is an enhanced echo. It is a limited variant of the C language
printf() function library, and its syntax is something different.

printf format-string... parameter...

This is the Bash builtin version of the /bin/printf or /usr/bin/printf command. See the
printf manpage (of the system command) for in-depth coverage.

Chapter 15. Internal Commands and Builtins

183