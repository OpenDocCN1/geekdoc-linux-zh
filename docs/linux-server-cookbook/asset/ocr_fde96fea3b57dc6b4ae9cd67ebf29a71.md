By having multiple CPUs available, the tasks are going to be distributed between different CPUs, and the load would be related to the number of CPUs. A system load of 3.00 having four processors indicates that it is using 66.67% of the available CPU resources.

# ## Command uptime and file /etc/loadavg

This command, described in Chapter 3, Using the Command Line Interface, to see how long the system was running, is used to have a simple overview. Command uptime shows the CPU load average in the system. The load average on Linux systems is represented for the periods of 1 minute, 5 minutes, and 15 minutes. Figure 6.6 illustrates the average in the last minute was 0.13, for the last 5 minutes it was 0.07, and for the last 15 minutes it was 0.01:

```
```
[root@server ~]# uptime
16:44:42 up 73 days, 10:00,  2 users,  load average: 0,13, 0,07, 0,01
```
```

![](bbox=[0.33, 0.41, 0.66, 0.43])

Most of the commands open the file /proc/loadavg to obtain information about the system load. This file contains the information for the periods described previously in the first three columns; the fourth column indicates, separated by a slash (/), how many processes are accessing to the CPU and how many processes are being executed in the system, and the last column indicates the last process id assigned. Figure 6.7 features a content example for the file /prod/loadavg:

![](bbox=[0.14, 0.57, 0.87, 0.64])

![](bbox=[0.33, 0.66, 0.66, 0.68])

# ## Command top

The command top provides a dynamic real-time information about the system. In Chapter 5, Managing Files, Directories, and Processes, this command was introduced to list the processes running in the system. The head part of the information shown is related to the system resources usage, as is illustrated in figure 6.8: