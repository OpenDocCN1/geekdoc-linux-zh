# Save configuration settings to ~/.toprc.

> A fancier and more user-friendly version of top is htop. Another —perhaps more exhaustive— alternative is atop. If not already installed in your system, use your package manager to install them and give them a try.

# An Explanation of the output of top

top output is divided into two areas: the summary area and the task area.

# The Summary Area in top

The summary area is made up of the the five top rows and gives us the following information:

+   ```
+   top - 11:10:29 up 2:21, 1 user, load average: 0,11, 0,20, 0,14
+   ```

+   * current time (in 24-hour format): 11:20:29

+   * uptime (how much time the system has been up and running): up 2:21

+   * number of users logged in and load average of the CPU for the last 1, 5 and 15 minutes, respectively: load average: 0,11, 0,20, 0,14

+   ```
+   Tasks: 73 total, 1 running, 72 sleeping, 0 stopped, 0 zombie
+   ```

+   * total number of processes in active mode: 73 total

+   * running (those being executed): 1 running

+   * sleeping (those waiting to resume execution): 72 sleeping

+   * stopped (by a job control signal): 0 stopped

+   * zombie (those which have completed execution but are still waiting for their parent process to remove them from the process table): 0 zombie

+   ```
+   %Cpu(s): 0,0 us, 0,3 sy, 0,0 ni, 99,7 id, 0,0 wa, 0,0 hi, 0,0 si, 0,0 st
+   ```

+   * user processes: 0,0 us

+   * system/kernel processes: 0,4 sy

+   * processes set to a nice value — the nicer the value, the lower the priority: 0,0 ni

+   * nothing — idle CPU time: 99,7 id

+   * processes waiting for I/O operations: 0,0 wa