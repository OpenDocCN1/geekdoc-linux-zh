- *Daemon process*—A system process that is not associated with a terminal or a graphical environment. It is a process or collection of processes that wait for an event to trigger an action on the part of the program. In network-based services, this event is a network connection. Other services, like cron and atd, are time-based and perform certain tasks at certain points in time.

Figure 10-2 illustrates the relationship between daemon processes and user processes.

![](bbox=[0.155, 0.19, 0.493, 0.536])

**Figure 10-2**

In this example, during the boot process of a Linux system, the init process launches several daemons (*daemon processes*), including a daemon for user login.

After the user logs on in a text console, a shell is started that lets him start processes manually (*user processes*). Within a graphical environment, he can open a terminal window from which he can start user processes, or he starts processes by clicking on icons or choosing from menus.

+   - *Process ID (PID)*—A unique identifier assigned to every process as it begins.
+   - *Child process*—A process that is started by another process (the parent process).
+   - *Parent process*—A process that started one or more processes (child processes).
+   - *Parent Process ID (PPID)*—The PID of the parent process that created the current process.