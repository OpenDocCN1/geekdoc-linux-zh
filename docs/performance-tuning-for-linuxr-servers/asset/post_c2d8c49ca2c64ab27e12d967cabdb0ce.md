
completing. For instance, some applications use a form of semaphore technique to dispatch work and wait for completion. Perhaps the work was dispatched to a back-end server or other application and that application has for some reason stopped processing all activity. As a result, the application closest to the user is blocked, not runnable, waiting on some semaphore to notify it of completion before it can return information to the user. This might cause the administrator to focus attention on the server application to see why it is unable to complete the requests being queued for it.

In another scenario, suppose that the load average is showing a load in excess of 1, possibly even a full point higher on average than established baselines. In addition, `vmstat` shows one or two processes always runnable, but the percentage of user time is nearly 100% over an extended period of time. Another tool might be necessary to find out what process or processes are using up 100% of the CPU timer (for instance, `ps(1)` or `top(1)` provides a listing of all processes that currently exist, or some selected subset of processes based on its options. `top(1)` (or `gtop(1)`) provides a constantly updating view of the most active processes, where *most active* can be defined as those processes that are using the most processor time. This data might help identify a runaway process that is doing nothing useful on the system. If `vmstat(1)` had reported that the processes were mostly running in user space, the administrator might want to connect a debugger such as `gdb(1)` to the process and use breakpoints, tracing, or other debugging means to understand what the application was doing. If `vmstat` had reported that most of the time was being consumed as "system" time, other tools such as `strace(1)` might be used to find out what system calls were being made. If `vmstat(1)` had reported that a large percentage of time was being spent waiting for I/O completion, tools such `sar(1)` could be used to see what devices were being used and also provide some possible insights into which applications or file systems were in use, whether the system were swapping or paging, and so on.

`vmstat(1)` provides some insights into the current state of the system. In this section, we looked at the areas that primarily interact with the CPU utilization. However, `vmstat(1)` also provides some insight into memory utilization, basic swapping activity, and I/O activity. Later sections in this chapter look at more of these areas in detail.

## top and gtop

`top` and `gtop` are very useful tools for understanding the tasks and processes that contribute to the high-level information provided by `vmstat` or `uptime`. They can show which processes are active and which ones over time are consuming the most processing time or memory.

The `top` command provides an updating overview of all running processes and the system load. `top` provides information on CPU load, memory usage, and usage per process, as detailed in the snapshot that follows. Note that it also provides load average snapshots much like `uptime(1)` does; however, `top` also provides a breakout of the number of processes that have been created but are currently sleeping, and the number of processes that are running. "Sleeping" tasks are those that are blocked waiting on some activity, such as a key press from a user at a keyboard, data from a pipe or socket, requests from another host (such as a web server waiting for someone to request content), and so on. `top(1)` also shows load average for each processor independently, which can help identify any imbalances in scheduling tasks. By default, the output of `top` is refreshed frequently, and tasks are sorted by percentage of CPU consumption. Other sorting options are possible, such as cumulative CPU consumption or percentage of memory consumption.

```
4:52pm  up  5:08,   3 users,   load average: 2.77, 5.81, 3.15
37 processes:  36 sleeping, 1 running, 0 zombie, 0 stopped
CPU0 states:  5.1% user, 53.1% system,  0.0% nice, 41.1% idle
CPU1 states:  5.0% user, 52.4% system,  0.0% nice, 41.4% idle
Mem:  511480K av, 43036K used, 468444K free,   0K shrd,  2196K
Swap: 263992K av,   0K used,  263992K free
PID USER   PRI  NI  SIZE  RSS  SHARE STAT %CPU %MEM   TIME COMMAND
1026 root    2    0   488  488  372   S  1.1  0.0 0:00 chat_s
7490 root   11    0  1012 1012  816   R  0.5  0.1 0:00 top
3  root   19   19   0    0    0    SWN  0.3  0.0 0:00 ksftirqd_C
4  root   19   19   0    0    0    SWN  0.1  0.0 0:00 ksftirqd_C
1  root    9    0   536  536  468   S  0.0  0.1 0:04 init
2  root    9    0   0    0    0    SW   0.0  0.0 0:00 keventd
5  root    9    0   0    0    0    SW   0.0  0.0 0:00 kswapd
6  root    9    0   0    0    0    SW   0.0  0.0 0:00 bdflush
7  root    9    0   0    0    0    SW   0.0  0.0 0:00 kupdated
9  root    9    0   0    0    0    SW   0.0  0.0 0:00 scsi_eh_0
10 root    9    0   0    0    0    SW   0.0  0.0 0:00 khubd
331 root   9    0   844  844  712   S  0.0  0.1 0:00 syslogd
341 root   9    0  1236 1236  464   S  0.0  0.2 0:00 klogd
356 rpc    9    0   628  628  536   S  0.0  0.1 0:00 portmap
```

top includes the following information in its output:

- Line 1 shows the system uptime, including the current time, how long the system has been up since the last reboot, the current number of users, and three load average numbers. The load average numbers represent the average number of processors ready to run during the previous 1, 5, and 15 minutes.
- Line 2 includes the process statistics, including the total number of processes running at the time of the last top screen update. This line also includes the number of sleeping, running, zombie, and stopped processes.
- Lines 3 and 4 display CPU statistics for individual CPUs, including the percentage of CPU time used by the user, system, nice, and idle processes.
- Line 5 provides memory statistics, including total memory available, used memory, free memory, shared memory by different processes, and memory used for buffers.
- Line 6 shows virtual memory or swap statistics, including total available swap space, used swap space, free swap space, and cached swap space.
- The remaining lines show statistics on the individual processes. Some of the more useful top parameters are as follows:
    - d: Delay between updates to the data.
    - p: Display only the processes specified. Up to 20 processes can be specified.
    - S: Display a summary of time being spent by the process and its children. Also displays dead time.
    - I: Do not report idle processes.
    - H: Show all threads by process.
    - N: Number of times to produce the reports.

top also has a dynamic mode to change report information. Activate dynamic mode by pressing the f key. By further pressing the j key, you can add a new column to show the CPU last used by an executing process. This additional information is particularly useful for understanding the process behavior in an SMP system.

This section barely scratches the surface of the types of information that top or gtop provide. For more information on top, see the corresponding man page; for more information on gtop, see the built-in help command.

## sar

sar is part of the sysstat package. sar collects and reports a wide range of system activity in the operating system, including CPU utilization, the rate of context switches and interrupts, the rate of paging in and paging out, the shared memory usage, the buffer usage, and network usage. sar(1) is useful because it constantly collects and logs system activity information in a set of log files, which makes it possible to evaluate performance problems both prior to the reporting of a performance regression event as well as after the event. sar can often be used to pinpoint the time of the event and can also be used to identify specific changes in the system's behavior. sar can also output information with a shorter interval or a fixed number of intervals, much like vmstat. Based on the values in the count and interval parameters, the sar tool writes information the specified number of times spaced at the specified intervals in seconds. In addition, sar can provide averages for a number of data points that it collects. The following example provides statistics on a four-way SMP system by collecting data every 5 seconds:

### CPU Utilization

```
11:09:13        CPU     %user   %nice   %system  %iowait   %idle
11:09:18        all     0.00     0.00      4.70     52.45    42.85
11:09:18            0     0.00     0.00      5.80     57.00    37.20
11:09:18            1     0.00     0.00      4.80     49.40    45.80
11:09:18            2     0.00     0.00      6.00     62.20    31.80
11:09:18            3     0.00     0.00      2.40     41.12    56.49
11:09:23        all     0.00     0.00      3.75     47.30    48.95
11:09:23            0     0.00     0.00      5.39     37.33    57.29
11:09:23            1     0.00     0.00      2.80     41.80    55.40
```
