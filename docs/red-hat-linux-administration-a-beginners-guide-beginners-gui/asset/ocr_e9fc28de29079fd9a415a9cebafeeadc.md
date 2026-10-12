+   * S Process is sleeping. All processes that are ready to run (that is, being multitasked, and the CPU is currently focused elsewhere) will be asleep.
+   * R Process is actually on the CPU.
+   * D Uninterruptible sleep (usually I/O related).
+   * T Process is being traced by a debugger or has been stopped.
+   * Z Process has gone zombie. This means either (1) the parent process has not acknowledged the death of its child using the **wait** system call; or (2) the parent was improperly **killed**, and until the parent is completely **killed**, the **init** process (see Module 8) cannot reap the child itself. A zombed process usually indicates poorly written software.

In addition, the STAT entry for each process can take one of the following modifiers: W = No resident pages in memory (it has been completely swapped out); < = High-priority process; N = Low-priority task; L = Pages in memory are locked there (usually signifying the need for real-time functionality).

+   * **Column 9: START** Date the process was started.
+   * **Column 10: TIME** Amount of time the process has spent on the CPU.
+   * **Column 11: COMMAND** Name of the process and its command-line parameters.

# ## Showing an Interactive List of Processes: top

The **top** command is an interactive version of **ps**. Instead of giving a static view of what is going on, **top** refreshes the screen with a list of processes every two to three seconds (user adjustable). From this list, you can reprioritize processes or **kill** them. Figure 6-1 shows a **top** screen.

The **top** program’s main disadvantage is that it’s a CPU hog. On a congested system, this program tends to complicate system management issues. Users start running **top** to see what’s going on, only to find several other people running the program as well, slowing down the system even more.

By default, **top** is shipped so that everyone can use it. You may find it prudent, depending on your environment, to restrict **top** to **root** only. To do this, change the program’s permissions with the following command:

```
`[root@workbox /root]# chmod 0700 /usr/bin/top`
```