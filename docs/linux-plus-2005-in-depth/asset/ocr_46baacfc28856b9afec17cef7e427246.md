```
[root@server1 root]# jobs
  [1]-  Running          sample &
  [2]+  Running          sample2 &
[root@server1 root]# kill -3 %
 /sbin/sample2: 7613 Quit
  [2]+  Exit 131             sample2
[root@server1 root]# jobs
  [1]+  Running          sample &
[root@server1 root]# kill -3 %
 /sbin/sample: 7605 Quit

  [1]+  Exit 131           sample
[root@server1 root]# jobs
[root@server1 root]#
```

# Process Priorities

Recall that Linux is a multitasking operating system; it can perform several different tasks at the same time. Because most computers contain only a single CPU, Linux executes small amounts of each process on the processor in series; this makes it seem to the user as if processes are executing simultaneously. The amount of time a process has to use the CPU is called a **time slice**; the more time slices a process has, the more time it has to execute on the CPU and the faster it executes. Time slices are typically measured in milliseconds; thus, several hundred processes can be executing on the processor in a single second.

The `ps -l` command lists the Linux kernel priority (**PRI**) of a process; this value is directly related to the amount of time slices a process has on the CPU. A PRI of 0 is the most likely to get time slices on the CPU, and a PRI of 127 is the least likely to receive time slices on the CPU. An example of this command is shown next:

```
[root@server1 root]# ps -l
  F S   UID   PID  PPID  C PRI  NI ADDR SZ WCHAN    TTY          TIME CMD
  4 S     0  3194  3192   0  75   0 -  1238 wait4    pts/1      00:00:00 bash
  4 S     0  3896  3194   0  76   0 -   953 -        pts/1      00:00:00 sleep
  4 S     0  3939  3194  13  75   0 -  7015 -        pts/1      00:00:01 gedit
  4 R     0  3940  3194   0  77   0 -   632 -        pts/1      00:00:00 ps
[root@server1 root]#
```

The `bash`, `sleep`, `gedit`, and `ps` processes all have different PRI values because the kernel automatically assigns time slices based on several factors. You cannot change the PRI directly, but can influence it indirectly by assigning a certain nice value to a process. A negative nice value increases the likelihood that the process will receive more time slices, whereas a positive nice value does the opposite. The range of nice values is depicted in Figure 10-4.