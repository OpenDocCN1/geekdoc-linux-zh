For the CPU, PATROL can show bottlenecks and utilization information, along with a variety of statistics, such as CPU idle time, run queue length, and swap queue length. Information about the operating system itself is also maintained, such as the name, version, and creation date.

PATROL can display the total number of processes, the number of zombie processes, and heavy CPU users. Through the PATROL console, you can perform administrative tasks, such as re-prioritizing processes.

PATROL also can display the total number of users and sessions, and can check security by monitoring the number of failed user and privileged logins. You can check the printer queue to see how many jobs are in the queue and to determine the state of the printer.

PATROL can monitor the filesystem and can automatically determine the effectiveness of the buffer cache. Regular reports can be generated to check disk usage per user, to create a list of the largest files, or to list files that have not been accessed in a long time. Corrective actions, such as removing core files, can also be configured.

In addition to the system metrics monitored by PATROL, the KM for UNIX includes a set of tools to provide additional system monitoring, including tools to monitor CPU usage, paging activity, I/O caching, swap activity, and system log files, tools to check filesystem and kernel file resources, and tools to monitor printer queues.

The following list shows some of the parameters available for monitoring from the PATROL KM for UNIX:

+   - CPUCpuUtil
- CPUIdleTime
- CPUInt
- CPULoad
- CPUProcsWaiting
- CPUProcSwch
- CPURunQSsize
- CPUSysTime
- CPUUserTime
- KERSysCall
- MEMActiveVirPage
- MEMFreeMem
- MEMPageAnticipated
- MEMPageFreed
- MEMPageIn
- MEMPageOut
- MEMPageScanned
- PRNQLength
- PROCAvgUsrProc