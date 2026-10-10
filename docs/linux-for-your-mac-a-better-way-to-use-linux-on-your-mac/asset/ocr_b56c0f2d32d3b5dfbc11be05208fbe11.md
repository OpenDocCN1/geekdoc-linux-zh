```
uniq >out.txt 2>>errors.txt &
(1) 31895
```

Note that in this example, the shell returned a number in brackets $(1)$, along with another number. The first number is called a job number, and is returned by the shell. The second number is a process id, and is returned by the Linux kernel. Knowing these numbers is important, because you can use either number to control the program in the background. This process is known as job control.

You can observe a list of running processes by using the ps command like this:

```
$ ps
PID TTY TIME CMD
772 tty1 00:00:00 bash
779 tty1 00:00:00 startx
780 tty1 00:00:00 tee
789 tty1 00:00:00 xinit
793 tty1 00:00:01 ksmserver
879 pts/0 00:00:00 cat
18158 pts/2 00:00:00 bash
21300 pts/2 00:00:00 telnet
29195 pts/3 00:00:00 bash
31861 pts/6 00:00:00 ah
31865 pts/6 00:00:00 less
31946 pts/5 00:00:00 pine
```

You can observe a list of current jobs by using the shell's jobs command like this:

```
$ jobs
[1]+ Stopped pine -z
[2]- Running find /usr -name . . .
```

In this example, two jobs are present, with one job suspended. Read on to learn more about using the shell and background tasks.

# Handling the Foreground and Background

One way to return a running background task, especially if you are using bash, is to use the fg (or foreground) built-in command. Using our previous example, type the command at the shell command line while the program is running in the background like this:

```
$ fg
find /usr -name README -print 2>errors.txt | \
```