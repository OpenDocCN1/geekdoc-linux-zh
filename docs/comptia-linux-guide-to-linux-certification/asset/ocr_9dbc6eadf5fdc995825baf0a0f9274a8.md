# Chapter 9  Managing Linux Processes

```
root 1213 1 0 21:31 ? 00:00:00 /usr/sbin/sshd -D
root 1216 1213 0 21:32 ? 00:00:00 sshd: root@pts/0
root 1220 1216 0 21:32 pts/0 00:00:00 -bash
root 1253 2 0 21:33 ? 00:00:00 [kworker/0:2]
root 1260 1 0 21:33 ? 00:00:00 /usr/libexec/packagekitd
root 1742 1220 0 21:33 pts/0 00:00:00 ps -ef
[root@server1 -]# _
```

As shown in the preceding output, the kernel thread daemon (kthreadd) has a PID of 2 and starts most subprocesses within the actual Linux kernel because those subprocesses have a PPID of 2, whereas the init daemon (/usr/lib/systemd/systemd, PID = 1) starts most other daemons because those daemons have a PPID of 1. In addition, there is a ? in the TTY column for daemons and kernel subprocesses because they do not run on a terminal.

Because the output of the ps -ef command can be several hundred lines long on a Linux server, you usually pipe its output to the less command to send the output to the terminal screen page-by-page, or to the grep command, which can be used to display lines containing only certain information. For example, to display only the BASH shells on the system, you could use the following command:

```
[root@server1 -]# ps -ef | grep bash
user1 2094 2008 0 01:29:35 pts/1 00:00:00 -bash
root 2159 2156 0 14:30 t2 00:00:00 -bash
root 2294 2159 0 14:44 t2 00:00:00 grep -color=auto bash
[root@server1 -]# _
```

Notice that the grep bash command is also displayed alongside the BASH shells in the preceding output because it was running in memory at the time the ps command was executed. This might not always be the case because the Linux kernel schedules commands to run based on a variety of factors.

The -e and -f options are the most common options used with the ps command; however, many other options are available. The -l option to the ps command lists even more information about each process than the -f option. An example of using this option to view the processes in the terminal tty2 is shown in the following output:

```
[root@server1 -]# ps -l
F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
4 S 0 2159 2156 0 80 0 - 1328 wait t2 00:00:00 bash
4 R 0 2295 2159 2 80 0 - 744 - t2 00:00:00 ps
[root@server1 -]# _
```

The process flag (F) indicates particular features of the process; the flag of 4 in the preceding output indicates that the root user ran the process. The process state (S) column is the most valuable to systems administrators because it indicates what the process is currently doing. If a process is not being run on the processor at the current time, you see an S (sleeping) in the process state column; processes are in this state most of the time, as seen with bash in the preceding output. You will see an R in this column if the process is currently running on the processor, or a T if it has stopped or is being traced by another process. In addition to these, you might also see a Z in this column, indicating a zombie process. When a process finishes executing, the parent process must check to be efficient if it executed successfully and then