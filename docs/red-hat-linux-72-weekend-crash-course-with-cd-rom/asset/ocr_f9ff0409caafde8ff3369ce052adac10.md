| Filename | Contents |
|---|---|
| /proc/uptime | Information about how long the system has been up. |
| /proc/version | Kernel version number. |

# ### Troubleshooting

In rare cases, top, gtop, or vmstat may not work. This usually happens when the /proc file system is not mounted because all three utilities use some of the files in /proc to display their reports. If this happens, reboot your system after shutting it down properly, of course. If you are having trouble viewing a file in /proc, it may be because you do not have read permissions on the file. Not all files in the /proc file system are world-readable, so use su to become the root user before looking at the file.

Similarly, disk usage statistics from the du command require read access to files and execute permissions for directories. If you try to use du on directories or files to which you do not have access, you will get an error message and the report it displays will not be accurate. Again, become the root user using the su command to solve the problem.

Finally, if hphram does not seem to be working, keep in mind that it requires root access because it accesses hardware directly.

![](bbox=[0.05, 0.57, 0.13, 0.63])

# ### REVIEW

This session showed you how to keep an eye on your Red Hat Linux system’s performance. You learned how to use and interpret the displays produced by top, the GNOME System Monitor, vmstat, and the uptime command. You also learned some commands to check the available disk space as well as your hard disk’s performance. Finally, you explored the /proc file system that contains an extensive amount of information about the system.

# ### QUIZ YOURSELF

+   1. What does the top utility do? (See “Using the top Utility.”)

+   2. How do you start the GNOME System Monitor? (See “Using the GNOME System Monitor.”)

+   3. What information does the vmstat utility provide? (See “Using the vmstat Utility.”)

+   4. Which program can you run to check the speed at which data can be read from your IDE hard disk? (See “Checking Disk Performance and Disk Usage.”)

+   5. What command do you use to view information about interrupt requests (IRQs) from the /proc file system? (See “Exploring the /proc File System.”)