# Chapter 7 Decisions, Decisions

In the case of grep, an exit status of zero (success) is returned if it finds the specified pattern in at least one of the files specified; a non-zero value is returned if it can't find the pattern or if a different error occurs, like failure to open a specified source file.

In a pipeline, the exit status reflects the last command in the pipe.

```
who | grep fred

grep exit status is used by the shell as the exit status for the whole pipeline. In this case, an exit status of zero (success) means that fred was found in who's output (that is, fred was logged on the time that this command was executed).
```

# The $ Variable

The shell variable $ is automatically set by the shell to the exit status of the last command executed. Naturally, you can use echo to display its value at the terminal.

```
$ cp phonebook phone2
$ echo $?
0 Copy "succeeded"
$ cp nosuch backup
cp: cannot access nosuch
$ echo $?
2 Copy "failed"
$ who See who's logged on
root console Jul 8 10:06
wilma tty02 Jul 8 12:36
barney tty04 Jul 8 14:57
betty tty15 Jul 8 15:03
$ who | grep barney
barney tty04 Jul 8 14:57
$ echo $?
0 Print exit status of last command (grep)
grep "succeeded"
$ who | grep fred
$ echo $?
1 grep "failed"
$ echo $?
0 Exit status of last echo
$
```

Note that the numeric result of a "failure" for some commands can vary from one version of Unix to the next, but success is always signified by a zero exit status.

Let's write a shell program called on that tells us whether a specified user is logged on to the system. The name of the user to check will be passed to the program on the command line. If the user is logged on, we'll print a message to that effect; otherwise we'll say nothing. Here is the program: