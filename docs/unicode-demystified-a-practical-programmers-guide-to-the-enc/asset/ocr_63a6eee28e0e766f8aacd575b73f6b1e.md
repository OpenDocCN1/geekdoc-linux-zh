# $ ps

```
PID TTY                     TIME CMD
2697 pts/0    00:00:02 bash
3299 pts/0    00:00:00 ps
```

With the -l (option) ps, displays more information about the processes:

# $ ps -l

```
FS UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
000 500 2697 2696 0 75 0      639 wait4 pts/0 00:00:02 bash
000 500 3330 2697 0 76 0      744      pts/0 00:00:00 ps
```

The -u option shows various types of information about the processes, including much of your CPU and memory each one is using:

# $ ps -u

```
USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
alex 2697 0.0 0.5 2556 1460 pts/0 S Jul31 00:02 -bash
alex 3330 0.0 0.2 2476 616 pts/0 S Jul31 00:00 -ps -u
```

The --forest option causes ps to display the main page as describes as an "ASCII process tree." It displays processes that are children of other processes indented under their parents, making the process hierarchy, and tree, easier to see:

# $ ps -ef --forest

```
UID PPID C STIME TTY TIME CMD
root 1 0 Jul22 ? 00:00:00 init
root 2 0 Jul22 ? 00:00:00 [kevent]
root 785 1 0 Jul22 ? 00:00:00 /usr/bin/apmd -p 10 -w 5 -W -P
alex 839 1 0 Jul22 ? 00:00:01 /usr/bin/sshd
root 3305 8 0 Aug01 ? 00:00:01 /usr/bin/sshd
alex 3307 8 0 Aug01 ? 00:00:00 /usr/bin/sshd
alex 3308 8 0 Aug01 ? 00:00:00 -bash
alex 3774 3 0 Aug01 ? 00:00:00 -ps -ef --forest
root 1040 1 0 Jul22 ? 00:00:00 login --root
root 3351 1 0 Aug02 ? 00:00:00 -bash
root 3402 3 1102 ?  0000:000 make modules
root 3416 4 0 Aug02 ? 00:00:00 make -C drivers CLFA
root 3764 4 0 Aug02 ? 00:00:00 make -C scsi modm
root 3773 3 0 Aug02 ? 00:00:00 1d -elf_if3
```

The next sequence of commands shows how to use ps to determine the process number of a process running in the background and how to terminate that process using the kill command. In this case it is not necessary to use ps, the shell displays the process number of the background processes. The ps utility verifies the PID number.

The first command executes in the background. The shell displays the job and PID numbers of processes, followed by a prompt: