![](bbox=[0.2, 0.14, 0.66, 0.37])

# Figure 28-2

Viewing current processes in the GNOME System Monitor window

The load averages give you an indication of how busy the system is. In addition to the top and GNOME System Monitor programs, you can also get the load averages with the uptime command, as follows:

```
uptime
  11:40am  up 2 days, 57 min,  3 users,  load average: 0.13, 0.23, 0.27
```

The output shows the current time, how long the system has been up, the number of users, and the three load averages. Load averages greater than 1 imply that many processes are competing for the CPU time simultaneously. You can then look at the top CPU processes and try to run these processes one after another (not all at the same time).

# Using the vmstat Utility

You can get summary information about the overall system usage with the vmstat utility. To view system usage information averaged over 5-second intervals, type the following command (the second argument indicates the total number of lines of output vmstat should display):

```
vmstat 5 8
      procs                       memory      swap            io     system      cpu
     r  b  w   swap  free  buff  cache   si   so    bi    bo   in   cs us sy id
     1  0  0  4724  1620  3420  18244    0    0     2     0  129  736 27  5 68
     3  0  0  4724  2068  3420  18244    0    0     0     2  124  179  3  8 89
     0  0  0  4724  2052  3420  18244    0    0     0     2  125  301 57 13 30
     0  0  0  4724  2124  3420  18232    0    0     0     3  134  213  6  8 86
```