# $!: PID NUMBER OF MOST RECENT BACKGROUND PROCESS

The shell expands $! to the value of the PID number of the most recent process that ran in the background. The following example executes sleep as a background task and uses echo to display the value of $!:

```
$ sleep 60 &
[1] 8376
$ echo $!
8376
```

# $?: EXIT STATUS

When a process stops executing for any reason, it returns an exit status to its parent process. The exit status is also referred to as a condition code or a return code. The shell expands the $? parameter to the exit status of the most recently executed command.

By convention, a nonzero exit status is interpreted as false and means the command failed; a zero is interpreted as true and indicates the command executed successfully. In the following example, the first ls command succeeds and the second fails; the exit status displayed by echo reflects these outcomes:

```
$ ls es
es
$ echo $?
0
$ ls xxx
ls: xxx: No such file or directory
$ echo $?
1
```

You can specify the exit status a shell script returns by using the exit builtin, followed by a number, to terminate the script. If you do not use exit with a number to terminate a script, the exit status of the script is that of the last command the script ran.

```
$ cat es
echo This program returns an exit status of 7.
exit 7
$ es
This program returns an exit status of 7.
$ echo $?
7
$ echo $?
0
```

The es shell script displays a message and terminates execution with an exit command that returns an exit status of 7, the user-defined exit status in this script. The first echo then displays the exit status of es. The second echo displays the exit status of the first echo: This value is 0, indicating the first echo executed successfully.