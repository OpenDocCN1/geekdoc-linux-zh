
Contrast that with the context of the actual daemon. The object role works with the actual daemon; you can review it with other daemons in the /usr/sbin directory. The vsftpd daemon works with the associated configuration file with the ftpd_t type. In contrast, the vsftpd daemon alone is executable with the ftpd_exec_t type.

```
-rwxr-xr-x. root root system_u:object_r:ftpd_exec_t:s0 /usr/sbin/vsftpd
```

The role of different daemons and their corresponding processes should match and contrast in a similar fashion. If they don’t, the daemon should not work, and the problem should be documented in the SELinux audit log described in Chapter 4 in the /var/log/audit directory.

## View Loads with the top Task Browser

The top command sorts active processes first by their CPU load and RAM memory usage. Take a look at Figure 9-7. It provides an overview of the current system status, starting with the current up time, number of connected users, active and sleeping tasks, CPU load, and more. The output is in effect a task browser.

The default sort field is CPU load. In other words, the process that’s taking the most in CPU resources is listed first. You can change the sort field with the help of the left and right directional (<, >) keys. Most of the columns are the same as shown in Figure 9-6, as detailed in Table 9-1. The additional columns are described in Table 9-2.

![](img/9139201cfcaf4292284a0eed074928e5_524_0.png)

### TABLE 9-2 Additional Columns of Output from top

| Column Title | Description |
|---|---|
| PR | The priority of the task; for more information, see the nice and renice commands |
| NI | The nice value of a task, an adjustment to the priority |
| VIRT | The virtual memory used by the task |
| RES | Physical memory in use by the process, not including swap space, in KB (similar to RSS in the output to the ps aux command) |
| SHR | Shared memory used by a task, which can be reallocated |
| S | Process status (same as STAT in the output to the ps aux command) |

One problem with the top and ps commands is that they display the status of processes on a system as a snapshot in time. That may not be enough. Processes may load a system for just a blip of time, or even periodic blips in time. One way to find more information about the overall load on a system is with two commands from the sysstat package: sar and iostat. That system activity information is logged courtesy of the sa1 and sa2 commands associated with the /etc/cron.d/sysstat script, which will be described shortly.

## System Activity Reports with the sar Command

The sar command, in essence, can be used to provide a system activity report. For example, Figure 9-8 shows the output of the sar -A command. As you can see, the output shows various CPU measures at different points in time. The default settings measure CPU load at ten-minute intervals. There are four CPU cores on this system, which are measured individually and as a whole. The large idle numbers shown in the figure are a good sign that the CPU is not being overloaded; however, the figure shows the load for less than an hour.

The ten-minute intervals associated with the sar command output are driven by a regular job in the /etc/cron.d directory. The output from those reports are collected in log files in the /var/log/sa directory. The filenames are associated with the numeric day of the month; for example, system activity report status for the fifteenth of the month can be found in the sa15 file in the noted directory. However, such reports are normally stored for the last seven days, based on the following default in the /etc/sysconfig/sysstat file:

```
HISTORY=7
```

### FIGURE 9-8 Output from the sar -A command

```
Linux 2.6.32-71.el6.x86_64_ (Maui)      01/24/2011      _x86_64_      (4 CPU)

12:00:01 AM  CPU   %usr   %nice   %sys   %iowait   %steal   %irq   %soft   %guest   %idle
12:10:01 AM  all    5.09    0.00    2.57     0.18     0.00    0.01    0.01    0.02    92.13
12:10:01 AM    0    4.69    0.00    4.15     0.07     0.00    0.02    0.01    0.04    91.01
12:10:01 AM    1    6.86    0.00    1.40     0.03     0.00    0.02    0.01    0.01    91.67
12:10:01 AM    2    4.00    0.00    3.44     0.55     0.00    0.09    0.01    0.02    91.97
12:10:01 AM    3    4.79    0.00    1.28     0.06     0.00    0.00    0.01    0.00    93.85
12:20:01 AM  all    5.41    0.00    2.74     0.24     0.00    0.02    0.01    0.02    91.56
12:20:01 AM    0    4.39    0.00    4.29     0.10     0.00    0.01    0.01    0.02    91.17
12:20:01 AM    1    7.98    0.00    1.54     0.03     0.00    0.04    0.01    0.00    90.40
12:20:01 AM    2    3.60    0.00    3.81     0.70     0.00    0.01    0.02    0.04    91.83
12:20:01 AM    3    5.69    0.00    1.33     0.11     0.00    0.00    0.01    0.00    92.85
12:30:01 AM  all    6.20    0.00    2.61     0.19     0.00    0.02    0.02    0.02    90.94
12:30:01 AM    0    5.31    0.00    4.53     0.05     0.00    0.03    0.02    0.03    90.03
12:30:01 AM    1    7.84    0.00    1.52     0.02     0.00    0.05    0.02    0.01    90.54
12:30:01 AM    2    4.36    0.00    3.21     0.63     0.00    0.00    0.03    0.03    91.75
12:30:01 AM    3    7.29    0.00    1.21     0.06     0.00    0.00    0.01    0.00    91.43
12:40:01 AM  all    4.80    0.00    2.38     0.22     0.00    0.01    0.02    0.02    92.56
12:40:01 AM    0    4.45    0.00    3.92     0.07     0.00    0.02    0.01    0.03    91.49
12:40:01 AM    1    6.31    0.00    1.27     0.01     0.00    0.07    0.01    0.01    92.32
12:40:01 AM    2    3.39    0.00    3.28     0.67     0.00    0.00    0.02    0.02    92.61
12:40:01 AM    3    5.03    0.00    1.06     0.11     0.00    0.00    0.00    0.00    93.79
```

## CPU and Storage Device Statistics with iostat

In contrast to sar, the iostat command reports more general input/output statistics for the system, not only for the CPU, but also for connected storage devices, such as local drives and mounted shared NFS directories. An example shown in Figure 9-9 displays information for the CPU and the storage devices on the server1.example.com system.

## Variations on sar with sa1 and sa2

The sa1 and sa2 commands are often used to collect system activity report data. In the /etc/cron.d/sysstat script, the sa1 command is used to gather disk activity data every ten minutes. In that same script, the sa2 command collects all sar data in a daily report. As noted in the script, that report is processed every day, at seven minutes before midnight.

## nice and renice

The nice and renice commands can be used to manage the priority of different processes. While the nice command is used to start a process with a different priority, the renice command is used to change the priority of a currently running process.

### FIGURE 9-9

```
[root@server1 ~]# iostat
Linux 2.6.32-71.el6.x86_64 (server1.example.com)      01/26/2011      _x86_64_
(2 CPU)
CPU and storage device statistics
avg-cpu:  %user   %nice %system %iowait  %steal %idle
           0.05    0.00    0.03    0.03    0.00 99.88

Device:            tps   Blk_read/s   Blk_wrtn/s   Blk_read   Blk_wrtn
sda               0.00       0.01       0.00      2368        0
sdb               0.00       0.01       0.00      2144        0
scd0              0.00       0.03       0.00      7392        0
vda               0.21       2.70       1.97    765626    556858
dm-0              0.00       0.00       0.00       256        0

[root@server1 ~]#
```

Process priorities in Linux specify numbers that seem counterintuitive. The range of available nice numbers can vary from -20 to 19. A process given a priority of -20 takes precedence over all other processes. In contrast, a process given a priority of 19 will wait until the system is almost completely free before taking any resources. The default nice number of a process is 0.

The nice command prefixes other commands. For example, if you have an intensive script to be run at night, you might choose to start it with a command like the following:

```
$ nice -n 19 ./intensivescript
```

This command starts the noted script with the lowest possible priority. If started at night (or at some other time when a system is not loaded by other programs), the script is run until just about any other jobs, such as a script in the /etc/cron.* directories, are scheduled for execution. As such scripts are run on a schedule, they normally should take priority over some user-configured programs.

Sometimes a program is just taking up too many resources. If you need to make sure that program continues to run, one step before killing the associated process is to lower its priority with the renice command. Normally, the easiest way to identify a process that's taking up too many resources is by its PID in the output to the top command. That PID number is in the left-hand column of the output. For example, if you identify a process that's monopolizing current CPU and memory resources, copy the PID number of that process. If that number were 1234, the following command would change the nice number of that process to -10, which gives that process a higher priority than the default of 0.

```
# renice -10 1234
```
