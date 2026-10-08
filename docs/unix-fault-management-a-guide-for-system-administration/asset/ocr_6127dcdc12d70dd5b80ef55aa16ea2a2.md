# **Figure 4-5** Using the SyMON Physical View to identify a failed hardware component.

![](bbox=[0.1, 0.13, 0.89, 0.5])

For the operating system, the agent includes modules to monitor CPU utilization, memory usage, directory size, file size and file modification time, MIB-II objects. NFS activity, inode usage, swap statistics, filesystem usage, and disk rates and service times. A file-scanning module also is available that can be used to check log files, such as the system log, for errors or specific patterns.

The Health Monitor uses rules based mostly on performance metrics to correlate the metrics to detect when alarm conditions exist. It sends an alarm when alarm conditions occur, along with suggested steps on how to improve system performance. The Health Monitor has rules to detect swap space conditions, kernel contention, CPU, disk, or memory bottlenecks, printer problems, and filesystem conditions.

SyMON agents provide active management, including active configuration management controls for dynamic reconfiguration, system domain management, and an “alternate pathing” feature for redirecting disk I/O in the event of a controller failure. With this capability, administrators can take care of repairs, such as replacing a failed memory board, without a service interruption.

Sun Enterprise Servers Models E3000 through UE10000, with Solaris 2.6 or greater, support dynamic reconfiguration. This feature enables you to replace boards online without taking down the system. You can have backup boards on standby and available for immediate use. Or, if a CPU or memory board fails, you can unconfigure and disconnect the failed board online via SyMON,