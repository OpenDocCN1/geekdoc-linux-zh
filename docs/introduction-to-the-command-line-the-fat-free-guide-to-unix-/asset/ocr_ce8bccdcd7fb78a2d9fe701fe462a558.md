# top

Purpose: Monitor system performance and running processes.

Usage syntax: top [OPTIONS]

```
$ top

```
top - 18:56:55 up 21 min, 2 users, load average: 0.22, 0.35, 0.31
Tasks: 140 total, 2 running, 138 sleeping, 0 stopped, 0 zombie
Cpu(s): 9.0%us, 2.0%sy, 0.1%ni, 85.1%id, 3.5%wa, 0.1%hi, 0.2%si, 0.0%st
Mem: 3988516k total, 1089196k used, 2899320k free, 35832b buffers
Swap: 3951948k total, 0k used, 3951948k free, 66484k cached

  PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
 5297 nick 20 0 19112 1224 892 R 4 0.0 0:00.02 top
 1 root 20 0 4100 920 632 S 0 0.0 0:01.16 init
 2 root 15 -5 0 0 0 S 0 0.0 0:00.00 kthread
 3 root RT -5 0 0 0 S 0 0.0 0:00.00 migration/0
 4 root 15 -5 0 0 0 S 0 0.0 0:00.82 ksoftirqd/0
 5 root RT -5 0 0 0 S 0 0.0 0:00.00 watchdog/0
 6 root RT -5 0 0 0 S 0 0.0 0:00.00 migration/1
 7 root 15 -5 0 0 0 S 0 0.0 0:00.00 ksoftirqd/1
 8 root RT -5 0 0 0 S 0 0.0 0:00.00 watchdog/1
 9 root 15 -5 0 0 0 S 0 0.0 0:00.01 events/0
 10 root 15 -5 0 0 0 S 0 0.0 0:00.04 events/1
 11 root 15 -5 0 0 0 S 0 0.0 0:00.00 khelper
```
Monitoring system activity with the top command
```

top is a process and performance monitor for Unix, Linux, and BSD systems. The first few lines of top output displays information about processor, memory, and swap utilization. The remaining portion of the screen is used to display information about running processes. The process listing updates every few seconds to display the most resource-intensive processes.

> **Tip** There are several interactive commands that can be used to control the output of the top command. Press the ? key within top for a complete listing of these commands.

Common usage examples:

| Command | Description |
| :--- | :--- |
| top | Monitor system performance and processes |
| top -u [USER] | Only display processes owned by the specified user |
| top -d [SECONDS] | Update at the specified interval (in seconds) |
| top -i | Do not display idle processes |