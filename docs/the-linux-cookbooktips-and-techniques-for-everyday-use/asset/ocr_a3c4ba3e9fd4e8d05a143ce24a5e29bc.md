# 3.7 Listing System Activity

When you run a command, you are starting a process on the system, which is a program that is currently executing. Every process is given a unique number, called its process ID, or "PID."

Use ps to list processes on the system. Some of the information it can display about a process includes process ID, name of command being run, username running the command, and how long the process has been running. By default, ps outputs 5 columns: process ID, the name of the terminal from which the process was started, the current status of the process (including `S` for sleeping, meaning that it is on hold at the moment, `R` meaning that it is running, and `Z` meaning that it is a zombie process, or a process that has already died), the total amount of time the CPU has spent on the process since the process started, and finally the name of the command being run.

The following recipes describe popular usage of ps.

+   3.7.1 Listing Your Current Processes
+   Listing your processes.
+   3.7.2 Listing All of a User's Processes
+   Listing someone else's processes.
+   3.7.3 Listing All Processes on the System
+   Listing all of the processes on the system.
+   3.7.4 Listing Processes by Name or Number
+   Listing processes by name or number.

# 3.7.1 Listing Your Current Processes

Type ps with no arguments to list the processes you have running in your current shell session.

+   To list the processes in your current shell session, type:

```
$ ps RET
  PID TTY STAT TIME COMMAND
  193  1 S  0:01 -bash
  204  1 S  0:00 ps
$
```

In this example, ps shows that two processes are running: the bash and ps commands.