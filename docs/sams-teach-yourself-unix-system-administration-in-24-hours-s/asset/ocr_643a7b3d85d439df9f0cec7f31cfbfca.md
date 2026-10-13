# Examining Processes with the ps Command

There are a number of different commands available for examining running processes, but the most important one is ps, or process status, which first showed up in Hour 6, "Account Management." Although it's littered with lots of flags, there's a standard set of two or three flags you'll use 99% of the time to find all processes running on the system.

Give ps a specific process ID and it'll tell you about that process, identify a terminal (or virtual terminal), and it'll tell you about every process associated with that terminal. Specify a user and it'll show you everything that user is running, and lots more.

# Task 14.2: Exploring ps

The ps command is somewhat akin to the ls command, in that it has dozens of different options, but most of them are safely ignored, except in unusual circumstances.

+   1. Enough talk, let's act! To start out, let's allow ps to tell us about our login shell:

```
# ps $$
PID TTY STAT TIME COMMAND
1636 pts/2 S 0:01 bash
```

Without any modifiers, the ps command reports the PID, the terminal associated with the process, its status, the amount of CPU time that the process has consumed so far, and the actual command itself. As you can see, I'm running the bash shell.

The most interesting column here is STAT, which is really the current status of the process. The value S indicates that it's sleeping, oddly enough, even though it's my current shell. (Don't worry, though; the shell itself sleeps while the ps command it spawned runs.)

A full list of different process states is shown in Table 14.1.

TABLE 14.1 ps Process States

| State | Meaning |
|---|---|
| D | Sleep (uninterruptible, blocked for input or output) |
| R | Runnable (in the "run queue") |
| S | Sleeping |
| T | Traced or stopped (often with ^Z by the user) |
| Z | A "zombie" process (defunct or ended, but still stuck in the process queue) |