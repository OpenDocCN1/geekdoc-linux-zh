Alt-F1 terminal is the one used by default. I find virtual terminals most useful when I am developing software – I can be editing code on one terminal, compiling the results on another and looking up information on yet a third.

In the previous ps listing, notice the numbers in the TTY column. They show which processes are associated with each of the virtual terminals (v01 to v06). Notice that the shell with the PID of 325 is the login shell for a user on virtual terminal one. However, the ps command which generated the output listing was executed by a user on virtual terminal two. The other four virtual terminals all have copies of the program

```
/sbin/getty
```

running against them. This is the program that gives you a login prompt and waits for you to enter your login name. See how all four copies of the program are running as separate processes (i.e. they all have different PIDs).

Normally, when a user logs out, all the processes controlled by the same terminal (in the TTY column) that the user was logged in to will be terminated. However, the processes that have a question mark (or query ‘?’) in the TTY column are all running without an associated terminal, which means that they can continue to run even when there are no users logged in.

If you want to find out quickly what terminal you are logged in to, you can do so by using the tty command:

```
$ tty
/dev/tty1
```

As you can see, the full name for virtual terminal 1 is /dev/tty1. Similarly, virtual terminal 2 would be /dev/tty2, and so on. If you remember, the /dev directory is where the system keeps its special files by convention, and the virtual terminals are one example of what the special files are used for.

Sometimes it can be necessary to force the termination of a process. As long as it is a process over which you have control, usually because you executed it, then it is a simple matter to terminate it using the kill command. All you do is to pass the PID of the process whose execution you wish to terminate as a parameter to the kill command and kill will then send a signal to the process to terminate it. It is possible for a process to ignore the default signal sent to it by kill, in which case a -9 switch to the kill command will send a signal that cannot be ignored. Consider the following command sequence, which demonstrates these points:

```
$ tty
/dev/tty2
$ ps
PID TTY STAT TIME COMMAND
325 v01 S 0:00 -bash
460 v02 S 0:00 -bash
557 v02 R 0:00 ps
```