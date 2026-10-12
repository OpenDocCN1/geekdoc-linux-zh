# Monitoring System Performance

If your Linux system is being used as a multiuser computer, sharing the processing power of that computer can be a major issue. Likewise, any time you can stop a runaway process or reduce the overhead of an unnecessary program running, your Linux server can do a better job serving files, Web pages, or e-mail to the people that rely on it.

Utilities are included with Linux that can help you monitor the performance of your Linux system. The kinds of features you want to monitor in Linux include CPU usage, memory usage (RAM and swap space), and overall load on the system. The following sections describe tools for monitoring Linux.

# Checking system load average with xload

One way of keeping an eye on general system performance is to open an xload window on your desktop and put it off in the corner somewhere. The load window graphically represents the performance of your system. It periodically checks the load on the system and then charts demand on the system over time.

By default, xload updates the display every 10 seconds. Scale lines on the window help you monitor when xload has exceeded certain limits. The label in the xload window shows the system name. By running xload windows from various host computers and displaying them on your screen, you can monitor a whole set of computers at once.

Figure 10-4 shows the xload window.

![](bbox=[0.1, 0.56, 0.24, 0.65])

Figure 10-4: Xload graphically represents performance of a Linux system.

# Monitoring CPU usage with top and gtop

Start the top utility in a terminal window, and it displays the top CPU consuming processes on your computer. Every five seconds, top will determine which processes are consuming the most CPU time and display them in descending order on your screen.

By adding the -s option to top, you can have the display show you the cumulative CPU time that the process, as well as any child processes that may already have exited, has spent. If you want to change how often the screen is updated, you can add the -d secs option, where secs is replaced by the number of seconds between updates.

If you prefer a more graphical version of top, try the Gnome System Monitor. You can start this monitor by typing the gtop command from a Terminal window. Because gtop is an X