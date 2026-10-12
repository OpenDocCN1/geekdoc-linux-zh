The first six lines of the output screen (refer to Figure 1-2) provide summary information about the system. Here is what these six lines show:

+   - The first line shows the current time, how long the system has been up, how many users are logged in, and three load averages — the average number of processes ready to run during the last 1, 5, and 15 minutes.
+   - The second line lists the total number of processes and the status of these processes.
+   - The third line shows CPU usage — what percentage of CPU time is used by user processes, what percentage by system (kernel) processes, and during what percentage of time the CPU is idle.
+   - The fourth and fifth lines show how the physical memory is being used — the total amount, how much is used, how much is free, how much is shared, and how much is allocated to buffers (for reading from disk, for example).
+   - The sixth line shows how the virtual memory (or swap space) is being used — the total amount of swap space, how much is used, how much is free, and how much is being cached.

The table that appears below the summary information (refer to Figure 1-2) lists information about the current processes, arranged in decreasing order by amount of CPU time used. Table 1-4 summarizes the meanings of the column headings in the table that top displays.

![](bbox=[0.12, 0.65, 0.22, 0.78])

If the RSS field is drastically smaller than the SIZE field for a process, the process is using too little physical memory compared to what it needs. The result is a lot of swapping as the process runs. You can use the vmstat utility (which I discuss later in this section) to find out how much your system is swapping.

Table 1-4 Meanings of Column Headings in top Utility's Output

| Heading | Meaning |
|---|---|
| PID | The process ID of the process |
| USER | Username under which the process is running |
| PRI | Priority of the process |
| NI | Nice value of the process — the value ranges from -20 (highest priority) to 19 (lowest priority) and the default is 0 |
| SIZE | Total size of the process, in kilobytes |
| RSS | Total physical memory used by a task (typically shown in kilobytes, but an M suffix indicates megabytes) |