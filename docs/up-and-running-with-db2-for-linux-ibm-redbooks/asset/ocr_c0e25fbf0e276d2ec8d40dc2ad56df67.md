comprehensive information provided by these operating system tools, combining database system monitoring tools from DB2 UDB, you can understand your system more clearly; for example, which table space containers are under high disk I/O pressure, whether or not the excessive sort heap allocation will lead to a mass of paging space activities, if the network bandwidth is the bottleneck for poor response time of client applications, and so on. Then you can make pertinent adjustments to your applications, database system, or operating system to improve the system performance.

In this section, we discuss some of the most commonly used performance monitoring tools for the Linux platform: top, iostat, vmstat, and sar.

# 6.3.1 Top

Top is a very useful tool that gives you a lot of information on one screen. Top can show you which process is taking the longest processor time, the largest amount of memory (both in percentages), plus how long the system has been up, and the amount of free memory. By default the utility will refresh the display every 5 seconds. You can override the default refresh interval via the command option "d". The users should be aware that the top command does not report total memory used for DB2 correctly. Top will overstate memory usage by counting shared memory segment multiple times.

> Note: In Linux, DB2 will not free shared memory automatically. To free the shared memory, you need to recycle DB2.

Some frequently used command line options for Top are listed in Table 6-1.

Table 6-1 Frequently used command options for Top

| Command option | Description |
|---|---|
| d | Specifies the delay between screen updates. |
| p | Monitors only processes with given process ID. This flag can be given up to twenty times. |
| i | Starts Top ignoring any idle or zombie processes. |
| c | Displays command line instead of the command name only. |
| b | Batch mode. Useful for sending output from Top to other programs or to a file. In this mode, Top will not accept command line input. It runs until it produces the number of iterations requested with the n option or until killed. Output is plain text suitable for display on a dumb terminal. |