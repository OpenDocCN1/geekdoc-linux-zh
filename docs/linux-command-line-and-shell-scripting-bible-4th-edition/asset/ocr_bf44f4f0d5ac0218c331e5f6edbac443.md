```
```
#!/bin/bash
# Testing a single parentheses condition
echo $BASH_SUBSHELL
#
if (echo $BASH_SUBSHELL)
then
    echo "The subshell command operated successfully."
#
else
    echo "The subshell command was NOT successful."
#
fi
$
$ ./SingleParentheses.sh
0
1
The subshell command operated successfully.
$
```
```

When the script runs the `echo $BASH_SUBSHELL` command the first time (prior to the `if` statement), it completes the operation within the current shell. The command displays a `0`, indicating there is no subshell in use. (The `$BASH_SUBSHELL` environment variable was covered in [Chapter 5].) Within the `if` statement, the script performs the command in a subshell and the `echo $BASH_SUBSHELL` command shows a `1`, indicating a subshell was used. This subshell operation completes successfully, triggering the `then` command.

> **WARNING**
> 
> **While you can use process lists (covered in Chapter 5) within the `if` test statement, unexpected results may occur. If all the process list’s commands fail except the last command, the subshell will set the exit status to zero, and the commands listed under the `then` section will run.**

Modifying the script slightly, here's an example of an unsuccessful command run in a subshell:

```
```
$ cat SingleParentheses.sh
```
```