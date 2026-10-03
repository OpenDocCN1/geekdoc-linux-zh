A dialog similar to that marked B in the above figure will appear when the button is clicked. Select a process from the list and click the End Process button (C) to terminate it.

To monitor CPU, memory, swap, and network usage, click on the Resources button in the title bar to display the screen shown in Figure 34-5:

![](bbox=[0.14, 0.17, 0.89, 0.42])

Figure 34-5

Similarly, a summary of storage space used on the system can be viewed by selecting the File Systems toolbar button:

![](bbox=[0.18, 0.51, 0.83, 0.6])

Figure 34-6

# 34.2 Real-time System Monitoring with top

As the chapter “An Overview of the Cockpit Web Interface” outlined, the Cockpit web interface can perform basic system monitoring. The previous section also explained how the GNOME System Monitor tool could be used to monitor processes and system resources. This chapter also explored how the ps command can provide a snapshot of the processes running on a RHEL 9 system. However, the ps command does not provide a real-time view of the processes and resource usage on the system. The top command is an ideal tool for real-time monitoring of system resources and processes from the command prompt.

When running, top will list the processes running on the system ranked by system resource usage (with the most demanding process in the top position). The upper section of the screen displays memory and swap usage information together with CPU data for all CPU cores. All of this output is constantly updated, allowing the system to be monitored in real-time: