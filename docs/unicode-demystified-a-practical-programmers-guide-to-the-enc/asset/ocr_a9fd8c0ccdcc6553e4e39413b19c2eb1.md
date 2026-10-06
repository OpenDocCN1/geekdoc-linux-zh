# 562 Chapter 12 The Shell II: The Bourne Again Shell

You can also use pstree to see the parent/child relationship of processes. The next example shows the -p option in pstree, which causes it to display PID numbers:

```
$ pstree -p
init(1)--ads1-connect(1591)--pppd(1619)--pppoe(1620)
 |-apmd(832)
 | |-atd(1148)
 | |-crond(1089)
 | |-gpm(1047)
 | |-httpd(1070)--httpd(1088)
 | |  '-httpd(1538)
 |
 | |-nfsd(1000)
 | |-nfsd(1001)
 | |-nmbd(1112)
 | |-ntpd(852)
 | |-portmap(686)
 | |-rhnsd(1170)
 | |-rpc.mount(989)
 | |-rpc.quotad(984)
 | |-rpc.stat(714)
 | |-rpciod(805)
 | |-sendmail(1028)
 | |-smbd(1107)--smbd(2118)
 | |-sshd(909)
 | |-syslogd(663)
 |  '-xinetd(942)
```

See the list starting on page 394 for information on some of the daemons by pstree. See "$PID Number" on page 586 for a description of how to instruct the shell to report on PID numbers.

# Executing a Command

When you give it a command, the shell usually forks (spawns) a child process to execute the command. While the child process is executing, the parent process sleeps. While a process is sleeping, it does not use any computer time but remains inactive, waiting to wake up. When the child process finishes executing the command, it tells its parent of its success or failure via the exit status and does. The parent process (which is running the shell) wakes up and prompts you for another command.

When you request that the shell run a process in the background by ending a command with an ampersand (&), the shell forks a child process without going to sleep and without waiting for the child process to run to completion. The parent process, executing the shell, reports the job number and PID number of the child, and prompts you for another command. The child process runs in the background, independent of its parent.