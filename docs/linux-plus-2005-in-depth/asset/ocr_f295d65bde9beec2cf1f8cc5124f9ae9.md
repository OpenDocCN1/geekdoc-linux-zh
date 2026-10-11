```
root 2839 2824 4 14:28 ? 00:00:38 /usr/X11R6/bin/X :0 -audit 0 -auth
/var/gdm/:0.Xauth -nolisten tcp v77
root 2901 2824 0 14:28 ? 00:00:01 gnome-session
root 3193 3192 0 14:29 ? 00:00:00 gnome-pty-helper
root 3194 3192 0 14:29 pts/1 00:00:00 bash
root 3232 2390 0 14:30 tty2 00:00:00 -bash
root 3429 3194 0 14:41 tty2 00:00:00 ps -ef
[root@server1 root]# _
```

As shown in the preceding output, the `init` daemon (PID=1) starts most other daemons because those daemons have a PPID of 1. In addition, there is a `?` in the TTY column for daemons because they do not run on a terminal.

Because the output of the `ps -ef` command can be several hundred lines long on a Linux server, you usually pipe its output to the `less` command to send the output to the terminal screen page-by-page, or to the `grep` command, which can be used to display lines containing only certain information. For example, to display only the BASH shells in the preceding output, you could use the following command:

```
[root@server1 root]# ps -ef | grep bash
root 3194 3192 0 14:29 pts/1 00:00:00 bash
root 3232 2390 0 14:30 tty2 00:00:00 -bash
root 3431 3194 0 14:44 tty2 00:00:00 grep bash
[root@server1 root]# _
```

Notice that the `grep bash` command is also displayed alongside the BASH shells in the preceding output because it was running in memory at the time the `ps` command was executed. This might not always be the case because the Linux kernel schedules commands to run based on a variety of different factors.

The `-e` and `-f` options are the most common options used with the `ps` command; however, many other options are available. The `-1` option to the `ps` command lists even more information about each process than the `-f` option. An example of using this option to view the processes in the terminal tty2 is shown in the following output:

```
[root@server1 root]# ps -1
F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
4 S 0 3232 3192 0 75 0 - 1238 wait4 tty2 00:00:00 bash
4 R 0 3438 3232 0 77 0 - 744 - tty2 00:00:00
[root@server1 root]# _
```

The process flag (`F`) indicates particular features of the process; the flag of `4` in the preceding output indicates that the root user ran the process. The **process state** (`S`) column is the most valuable to systems administrators because it indicates what the process is currently doing. If a process is not being run on the processor at the current time, you see an S (sleeping) in the process state column; processes are in this state most of the time, as seen with `bash` in the preceding output. You will see an R in this column if the process is currently running on the