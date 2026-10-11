Throughout this textbook, you have examined various areas of a Linux system. In this chapter, you focus on fixing common problems that affect these areas. First, you explore system maintenance and troubleshooting procedures. Next, you learn about common hardware–related and software–related problems and their solutions, followed by a discussion of performance–related problems and utilities that can be used to monitor performance. Finally, you learn how to provide support for hardware and kernel features using modules, as well as how to compile this support directly into a new kernel.

# # Troubleshooting Methodology

After you have successfully installed Linux, configured services on the system, and documented settings, you must maintain the system’s integrity over time. This includes monitoring, proactive maintenance, and reactive maintenance, as illustrated in Figure 13-1.

![](bbox=[0.17, 0.51, 0.82, 0.83])

**Monitoring** is the activity on which Linux administrators spend the most time; it involves examining log files and running performance utilities periodically to identify problems and their causes. **Proactive maintenance** involves taking the necessary steps required to minimize the chance of future problems as well as their impact. Performing regular system backups and identifying potential problem areas are examples of proactive maintenance. All proactive maintenance