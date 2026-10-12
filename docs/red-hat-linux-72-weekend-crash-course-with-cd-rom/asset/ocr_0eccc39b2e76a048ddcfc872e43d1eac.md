# Using the GNOME System Monitor

Like the text-mode top utility, the **GNOME System Monitor** tool also enables you to view the system load in terms of the number of processes that are currently running, their memory usage, and the free disk space on your system. To run the tool, select *Main Menu* *Programs* *System* *System Monitor*. You can also start the tool by typing gtop in a terminal window. The tool starts and displays its output in the Processes tab of its main window, as shown in Figure 28-2.

![](bbox=[0.1, 0.28, 0.9, 0.55])

This output resembles what you see when you type top in a text-mode console or a terminal window. In fact, the column headings in the table match what the top utility uses in its output. As with the text-mode top utility, the display keeps updating to reflect the current state of the system. You see the current processes in descending order of CPU usage.

The **GNOME System Monitor** window has two more tabs that display the memory usage and the free space on the file system. To view this information, click the appropriate tab. For example, to see how various processes are using memory, click the **Memory Usage** tab.

The bottom of the window shows the CPU usage summary, system up time (how long the system has been up and running), and load averages (the average number of processes ready to run in the last 1, 5, and 15 minutes).

The load average gives you an indication of how busy the system is. In addition to the top and GNOME System Monitor programs, you can also get the load average with the *uptime* command, as follows:

```
uptime
11:40am up 2 days,  57 min,   3 users,  load average:  0.13,  0.23,  0.21
```

The output shows the current time, how long the system has been up, the number of users, and the three load averages. Load averages greater than 1 imply that multiple processes are competing for the CPU time simultaneously.