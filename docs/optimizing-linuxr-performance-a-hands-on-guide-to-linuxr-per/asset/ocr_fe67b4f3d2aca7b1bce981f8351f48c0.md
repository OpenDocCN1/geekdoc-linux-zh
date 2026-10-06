# ## 4.2. The Tools

Linux has a variety of tools to help determine which pieces of an application are the primary users of the CPU. This section describes these tools.

# ### 4.2.1. time

The time command performs a basic function when testing a command's performance, yet it is often the first place to turn. The time command acts as a stopwatch and knows how long a command takes to execute. It measures three types of time. First, it measures the real or elapsed time, which is the amount of time between the program started and finished execution. Next, it measures the user time, which is the amount of time that the CPU spent executing code on behalf of the program. Finally, time measures system time, which is the amount of time the CPU spent system or kernel code on behalf of the application.

# #### 4.2.1.1 CPU Performance-Related Options

The time command (see Table 4-1) is invoked in the following manner:

```
time [-v] application
```

# ### Table 4-1. time Command-Line Options

| Option | Explanation

+   - -v This presents a verbose display of the program's time and statistics. Some statistics are zeroed out, but more statistics are valid with Linux kernel v2.6 than with Linux kernel v2.4.

Most of the valid statistics are present in both the standard and verbose mode, but the verbose provides a better description for each statistic.

The application is timed, and information about its CPU usage is displayed on standard output after it has completed. Table 4-2 describes the valid output that the time command provides. The rest are not measured and always display zero.

# ### Table 4-2. CPU-Specific time Output

| Column | Explanation

+   - User time (seconds) This is the number of seconds of CPU spent by the application.

+   - System time (seconds) This is the number of seconds spent in the Linux kernel on behalf of the application.

+   - Elapsed (wall-clock) time (h:mm:ss or ms) This is the amount of elapsed time (in wall-clock time) between the application was launched and when it completed.

+   - Percent of CPU this job got This is the percentage of the CPU that the process consumed as it was running.