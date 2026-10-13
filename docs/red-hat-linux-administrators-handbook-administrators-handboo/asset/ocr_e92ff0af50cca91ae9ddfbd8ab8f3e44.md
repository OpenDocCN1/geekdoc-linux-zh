+   - Line 1. The uptime line, which shows the current time of the system, how long the system has been up since the last reboot, how many users are currently on the system, and three load average numbers. The load averages are the average numbers of processes ready to run during the last 1, 5, and 15 minutes.
+   - Line 2. The process statistics line that shows the total number of processes running at the time of the last top screen update. This line also shows the number of sleeping, running, zombie, and stopped processes.
+   - Line 3. Displays CPU statistics, which include percentage of CPU time used by the user, system, niced, and idle processes.
+   - Line 4. Provides memory statistics, which include total available memory, free memory, used memory, shared memory, and memory used for buffers.
+   - Line 5. Provides virtual memory or swap statistics, which include total available swap space, used swap space, free swap space, and cached swap space. The rest of the lines are similar to a ps-generated report.

Using top, you can identify which processes are using most of your resources, simply by looking at the few entries in the ps-like output. The process that consumes the second-most resources is the top utility itself! When you run top to monitor other processes, top takes some resources to run, but you still get a good idea about which process is consuming how much resources. To exit top, type 'q' at any time.

# Task Automation Commands

The commands discussed in this section show you how to run unattended tasks.

# at

The at utility allows you to queue a command for execution at a later time. For example, to run the disk usage summary generator utility called du at 8:40 p.m., you can run at as follows:

```
at 20:40
```