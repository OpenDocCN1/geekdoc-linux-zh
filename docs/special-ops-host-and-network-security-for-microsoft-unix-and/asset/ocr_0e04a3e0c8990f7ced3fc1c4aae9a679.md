# 546 Chapter 10 - Securing IIS

long wait for a Transmission Control Protocol (TCP) connection to time out, and you may want to consider using a much lower number here. Also, be sure that Enable Logging is checked.

# Figure 10.14 Web Site Properties

![](bbox=[0.298, 0.183, 0.692, 0.423])

Next, click Properties to bring up the Extended Logging Properties screen, shown in Figure 10.15. On the Extended Logging Properties, you may want to consider using local time for file naming and rollover. IIS always determines log entries in Coordinated Universal Time (UTC time), which will be determined based on your system clock and time zone settings. However, by using local time for file naming and rollover, the log files themselves will be cut off at midnight local time and a new log file created. From this screen, you may want to relocate your log files. The administrative partition mentioned earlier in the section "Preparing the File System" a good location for storing IIS log files.

# Figure 10.15 Extended Logging Properties

![](bbox=[0.328, 0.696, 0.672, 0.903])

www.syngress.com