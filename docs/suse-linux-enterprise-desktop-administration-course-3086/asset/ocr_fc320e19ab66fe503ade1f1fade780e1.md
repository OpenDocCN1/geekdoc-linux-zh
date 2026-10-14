Figure 10-3 illustrates the relationship between parent and child process ID numbers.

![](bbox=[0.126, 0.114, 0.647, 0.369])

Figure 10-3

For example, Process #1 is assigned a PID of 134. This process launches Process #2 with a PID of 291 and Process #3 with a PID of 348.

Because Process #1 launched Process #2 and Process #3, the second and third processes are considered *child processes* of Process #1 (the *parent process*). The PPID of Process #2 and #3 is the PID of process #1—134.

# Learn Jobs and Processes

In Linux, you use a *job identifier* (commonly called a *job ID*) to refer to processes when launching processes at the command-line. The job identifier is a numeric value that identifies the running program uniquely within that shell.

Independent of the shell, each process is identified using a *process ID* (commonly called a *PID*) that is unique across the entire system. All jobs have a PID, but not all processes have a usable job ID.

PID 1 always belongs to the init process. This is the first process started on the system and it creates a number of other processes, which, in turn, can generate additional processes.

If the highest possible PID within a system has been reached, the next process is allocated the lowest available number (such as PID 17494). Processes run for different lengths of time. After one process has ended, its number again becomes available.

When performing tasks such as changing the priority level of a running program, you use the PID instead of the job ID.

When you want to switch a process from the background to the foreground (and the process was started from a terminal), you use the job ID.

The use of PID and job ID is explained in more detail in “Manage Foreground and Background Processes” and “View and Prioritize Processes.”