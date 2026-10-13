# FIGURE 9-8 Output from the sar -A command

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

# CPU and Storage Device Statistics with iostat

In contrast to sar, the iostat command reports more general input/output statistics for the system, not only for the CPU, but also for connected storage devices, such as local drives and mounted shared NFS directories. An example shown in Figure 9-9 displays information for the CPU and the storage devices on the server1.example.com system.

# Variations on sar with sa1 and sa2

The sa1 and sa2 commands are often used to collect system activity report data. In the /etc/cron.d/sysstat script, the sa1 command is used to gather disk activity data every ten minutes. In that same script, the sa2 command collects all sar data in a daily report. As noted in the script, that report is processed every day, at seven minutes before midnight.

# nice and renice

The nice and renice commands can be used to manage the priority of different processes. While the nice command is used to start a process with a different priority, the renice command is used to change the priority of a currently running process.