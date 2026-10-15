
```
$ ps
    PID TTY      TIME CMD
14244 pts/1    00:00:00 bash
14572 pts/1    00:00:00 ps
```

You will notice that it always contains a line for the command itself because it itself has to run to do its job, obviously. The -f option causes it to display a full listing:

```
$ ps -f
UID       PID  PPID  C STIME TTY          TIME CMD
sweiss   2508  2507  0 12:09 pts/8    00:00:00 -bash
sweiss   3132  2508  0 12:22 pts/8    00:00:00 ps -f
```

The UID column is the user login name. The PID column is the process id of the process. The PPID column is the parent process's process id. The C field is rarely of interest; it gives processor utilization information. The STIME field is the starting time in hours, minutes, and seconds. The TIME column is the cumulative execution time, which for short commands will be zero, since the smallest unit of measurement in this column is seconds. The CMD column is the command line being executed by this process; in this case there are two: bash and "ps -f". All command line arguments are displayed; if any are suppressed, the command will appear in square brackets:

```
root      3080   1  0 Jan29 ?        00:00:00 [lockd]
```

The TTY column is the controlling terminal attached to this process. Some processes have no terminal, in which case a "?" will appear.

The -e option displays all processes, which will be quite long. If I want to know which process is the parent of my bash process, I can use ps -ef and filter using grep:

```
$ ps -ef | grep 2507
sweiss  2507  2504  0 12:09 ?        00:00:00 sshd: sweiss@pts/8
sweiss  2508  2507  0 12:09 pts/8    00:00:00 -bash
sweiss  3207  2508  0 12:30 pts/8    00:00:00 grep 2507
```

```
$ ps -ef | head -4
UID PID PPID C STIME TTY TIME CMD
root 0 0 0 Mar 13 ? 0:23 sched
root 1 0 0 Mar 13 ? 0:00 /etc/init -
root 2 0 0 Mar 13 ? 0:00 pageout
```

Notice that in Solaris, the (CPU) process scheduler itself is the very first process in the system. It is absent in Linux. In all UNIX systems, the process with PID 1 is always init. In Solaris, the pageout process is responsible for writing pages to disk, and fsflush flushes system buffers to disk.

The -u and -U options are useful for viewing all of your processes or those of others in a supplied user list. The list of users must be comma-separated, with no intervening spaces. For example:

```
$ ps -f -U sweiss,wgrzemsk
UID PID PPID C STIME TTY TIME CMD
sweiss 2507 2504 0 12:09 ? 00:00:00 sshd: sweiss@pts/8
sweiss 2508 2507 0 12:09 pts/8 00:00:00 -bash
wgrzemsk 2572 2570 0 12:10 ? 00:00:00 sshd: wgrzemsk@notty
wgrzemsk 2575 2573 0 12:10 ? 00:00:00 /bin/sh
```

While there are dozens of other options, I will only mention one more: the -o option. You can customize the output of the ps command to include any of the dozens of attributes available to be displayed using -o. The man page gives the general format for this. Some examples from the man page:

```
ps -eo pid,tid,class,rtprio,ni,pri,psr,pcpu,stat,wchan:14,comm
ps axo stat,euid,ruid,tty,tpgid,sess,pgid,ppid,pid,pcpu,comm
ps -eopid,tt,user,fname,tmout,f,wchan
```

Note that there are no spaces in the list. In general never use spaces in any of the lists because the shell will then treat them as separate words rather than a single word to be passed to the ps command itself.

A related command is pgrep. If you need the process id of a command or program that is running, typing pgrep <executable name> will give you a list of processes running that program, one per line. For example

```
$ pgrep bash
2508
3502
3621
```

showing that three instances of bash are running, with pids 2508, 3502, and 3621.

## 7.3 Process Groups

UNIX systems allow processes to be placed into groups. There are several reasons for grouping processes. One is that a signal can be sent to an entire process group rather than a single process. For example, the shell arranges that all processes created in order to carry out the command line are in a single group, so that if the user needs to terminate that command, a single signal sent via Ctrl-C will kill all processes in the group. The alternative would require using the ps command to find all processes that were created to carry out the command.

Every process has a process group-id (of type pid_t). There is a single process in each group that is considered to be the leader of the group. It can be identified easily, because it is the only process whose process group-id is the same as its process-id. You can view the process group-id of a process in the output of ps by using the -o option and specifying the format in either AIX format, such as

```
ps -o'%U %p %P %r %C %x %y %a'
```

or in standard format, as in

```
ps -ouser,pid,ppid,pgrep,%cpu,cputime,tty,args
```

If you run the command

```
$ cat | sort -u | wc
```

and then view the processes using one of the above ps commands, you will see the group formation:

```
$ psag -u sweiss | egrep 'TIME|cat|sort|wc'
USER PID PPID PGID %CPU TIME TTY COMMAND
sweiss 17198 17076 17198 0.0 00:00:00 pts/2 cat
sweiss 17199 17198 17198 0.0 00:00:00 pts/2 sort -u
sweiss 17200 17076 17198 0.0 00:00:00 pts/2 wc
```

Notice that the cat command's process group-id (pgid) is the same as its process-id (pid) and that the three processes belong to the same group. If the full listing were displayed you would see that no other process is in this group.

## 7.4 Foreground and Background Processes

UNIX allows processes to run in the foreground or in the background. Processes invoked from a shell command line are foreground processes, unless they have been explicitly placed into the background by appending an ampersand '&' to the command line. There can be only one process group in the foreground at any time, because you cannot enter a new command until the currently running one terminates and the shell prompt returns. Foreground processes can read from and write to the terminal.
