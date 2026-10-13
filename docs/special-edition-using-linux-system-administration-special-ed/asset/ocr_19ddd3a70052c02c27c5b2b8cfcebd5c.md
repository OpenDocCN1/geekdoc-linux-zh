# Monitoring Processes with the `ps` Command

The ps utility is used to display information about processes running on the system. Using this tool, it is possible to display the UID, PID, PPID, priority, controlling terminal (TTY), current status, percentage of CPU usage, percentage memory usage, start time, CPU time, and other information about current processes. The ps man page provides complete details of all the information about processes that can be displayed using the ps command.

# Process States

The ps program can be used to learn the current state of a process. At any given time, a process can be in one of five states as outlined in Table 8.2.

**Table 8.2 Process States**

| State | Description |
|---|---|
| Runnable | A runnable process is a process waiting in the scheduler’s run queue. It has all the resources it needs and is just waiting for CPU time. |
| Sleeping | A sleeping process is waiting for something to occur. An interactive shell sleeps waiting for terminal input. A process might be sleeping waiting for a file read or write to complete. A daemon might be sleeping till someone needs service and the kernel wakes it up. A sleeping process is woken up by a signal. Signals are discussed later in this chapter. |
| Swapped | A swapped process is one that has been completely removed from the computer’s main memory and been written out to disk. |
| Zombie | A zombie process is one that has died but did not exit cleanly and some shreds of information about this dead process are still lurking around in the kernel’s data structures. For all practical purposes, zombies can be safely ignored. Sometimes a zombie disappears after its parent process exits. In most cases, though, the only way to clean up zombies is to reboot the system. |
| Stopped | A stopped process is one that is marked as not runnable by the kernel. The best example of a stopped process is when you press Ctrl+Z during an interactive process running in bash or csh. The process stops running until you put it in the background using the shell’s bg (for background) command, at which time the process resumes in the background and you can proceed to use the shell interactively for another purpose. This process of stopping a program (and later resuming it) is discussed later in this chapter, in the section “Linux Signals.” |

# Sample `ps` Output

The ps program can display process information in a highly variable fashion depending on the arguments used with the command. In its most basic form, the ps command displays a simple list of processes which the user executing the command has running in the current terminal (tty). It doesn’t display processes owned by any other user.