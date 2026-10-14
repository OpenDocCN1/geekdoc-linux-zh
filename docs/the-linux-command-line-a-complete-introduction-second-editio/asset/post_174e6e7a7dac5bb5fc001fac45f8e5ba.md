
## State Meaning

| State | Meaning |
|-------|---------|
| D | Uninterruptible sleep. The process is waiting for I/O such as a disk drive. |
| T | Stopped. The process has been instructed to stop. You’ll learn more about this later in the chapter. |
| Z | A defunct or “zombie” process. This is a child process that has terminated but has not been cleaned up by its parent. |
| < | A high-priority process. It’s possible to grant more importance to a process, giving it more time on the CPU. This property of a process is called niceness. |
| N | A low-priority process. A process with low priority (a nice process) will get processor time only after other processes with higher priority have been serviced. |

A process with high priority is said to be less nice because it’s taking more of the CPU’s time, which leaves less for everybody else.

The process state may be followed by other characters. These indicate various exotic process characteristics. See the ps man page for more details.

Another popular set of options is aux (without a leading dash). This gives us even more information.

```
[me@linuxbox ~]$ ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.0   2136   644 ?        Ss   Mar05   0:31 init
root         2  0.0  0.0      0     0 ?        S<   Mar05   0:00 [kt]
root         3  0.0  0.0      0     0 ?        S<   Mar05   0:00 [mi]
root         4  0.0  0.0      0     0 ?        S<   Mar05   0:00 [ks]
root         5  0.0  0.0      0     0 ?        S<   Mar05   0:06 [wa]
root         6  0.0  0.0      0     0 ?        S<   Mar05   0:36 [ev]
root         7  0.0  0.0      0     0 ?        S<   Mar05   0:00 [kh]
--snip--
```

This set of options displays the processes belonging to every user. Using the options without the leading dash invokes the command with

“BSD-style” behavior. The Linux version of ps can emulate the behavior of the ps program found in several different Unix implementations. With these options, we get the additional columns shown in Table 10-2.

## Table 10-2: BSD Style ps Column Headers

| Header | Meaning |
|---|---|
| USER | User ID. This is the owner of the process. |
| %CPU | CPU usage in percent. |
| %MEM | Memory usage in percent. |
| VSZ | Virtual memory size. |
| RSS | Resident set size. This is the amount of physical memory (RAM) the process is using in kilobytes. |
| START | Time when the process started. For values over 24 hours, a date is used. |

## Viewing Processes Dynamically with top

While the ps command can reveal a lot about what the machine is doing, it provides only a snapshot of the machine's state at the moment the ps command is executed. To see a more dynamic view of the machine's activity, we use the top command.

```
[me@linuxbox ~]$ top
```

The top program displays a continuously updating (by default, every three seconds) display of the system processes listed in order of process activity. The name top comes from the fact that the top program is used to see the “top” processes on the system. The top display consists of two parts: a system summary at the top of the display, followed by a table of processes sorted by CPU activity.

```
top - 14:59:20 up 6:30, 2 users, load average: 0.07, 0.02, 0.00
Tasks: 109 total, 1 running, 106 sleeping, 0 stopped, 2 zombie
```

```
Cpu(s):  0.7%us,  1.0%sy,  0.0%ni, 98.3%id,  0.0%wa,  0.0%hi,  0.0%si
Mem:    319496k total,   314860k used,   4636k free,   19392k buff
Swap:   875500k total,  149128k used,  726372k free,  114676k cach

    PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM     TIME+  COMMAND
    6244 me       39  19 31752 3124 2188 S  6.3  1.0 16:24.42 trackerd
    11071 me      20   0 2304 1092  840 R  1.3  0.3  0:00.14 top
    6180 me       20   0 2700 1100  772 S  0.7  0.3  0:03.66 dbus-daemon
    6321 me       20   0 20944 7248 6560 S  0.7  2.3  2:51.38 multiloa
    4955 root     20   0 104m 9668 5776 S  0.3  3.0  2:19.39 Xorg
      1 root     20   0 2976  528  476 S  0.0  0.2  0:03.14 init
      2 root     15  -5    0    0    0 S  0.0  0.0  0:00.00 kthreadd
      3 root     RT  -5    0    0    0 S  0.0  0.0  0:00.00 migration
      4 root     15  -5    0    0    0 S  0.0  0.0  0:00.72 ksoftirq
      5 root     RT  -5    0    0    0 S  0.0  0.0  0:00.04 watchdog
      6 root     15  -5    0    0    0 S  0.0  0.0  0:00.42 events/0
      7 root     15  -5    0    0    0 S  0.0  0.0  0:00.06 khelper
     41 root     15  -5    0    0    0 S  0.0  0.0  0:01.08 kblockd/
     67 root     15  -5    0    0    0 S  0.0  0.0  0:00.00 kseriod
    114 root     20   0    0    0    0 S  0.0  0.0  0:01.62 pdfflush
    116 root     15  -5    0    0    0 S  0.0  0.0  0:02.44 kswapd0
```

The system summary contains a lot of good stuff. Table 10-3 provides a rundown.

## Table 10-3: top Information Fields

| Row Field | Meaning |
|---|---|
| 1 top | This is the name of the program. |
| 14:59:20 | This is the current time of day. |
| up 6:30 | This is called *uptime*. It is the amount of time since the machine was last booted. In this example, the system has been up for six and a half hours. |
| 2 users | There are two users logged in. |
| load average: | *Load average* refers to the number of processes that are waiting to run; that is, the number of processes that are in a runnable state and are sharing the CPU. Three values are shown, each for a different period of time. The first is the average for the last 60 seconds, the next the previous 5 minutes, and finally the previous 15 minutes. Values less than 1.0 indicate that the machine is not busy. |
