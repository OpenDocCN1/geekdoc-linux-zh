# 996 CHAPTER 27 PROGRAMMING THE BOURNE AGAIN SHELL

$ The shell stores the value of the PID number of the last process that ran in the background with $!. The following example executes sleep as a background task and uses echo to display the value of $!

```
$ sleep 60 &
[1] 8376
$ echo $!
8376
```

# $?: EXIT STATUS

When a process stops executing for any reason, it returns an exit status to its parent process. The exit status is also referred to as a condition code or a return code. The $? variables store the exit status of the last command.

By convention a nonzero exit status represents a false value and means the command failed. In the following-example, the first command succeed and the second fails, as demonstrated by the exit status:

```
$ ls es
es
$ echo $?
0
$ ls xxx
ls: xxx: No file or directory
$ echo $?
```

You can specify the exit status that a shell script returns by using the exit builtin, followed by a number, to terminate the script. If you do not use exit with a number to terminate the script, the exit status of the script is that of the last command the script ran.

```
$ cat es
echo This program returns an exit status of 7.
exit 7
$ es
This program returns an exit status of 7.
$ echo $?
7
$ echo $?
```

The shell script displays a message and terminates execution with an exit command that returns an exit status of 7, the user-defined exit status in this script. The first echo displays the value of exit status of es. The second displays the value of the exit status of the first echo. This value is 0, indicating the first echo was successful.

# POSITIONAL PARAMETERS

Positional parameters comprise the command name and command-line arguments. These parameters are called positional because within a shell script, you refer to