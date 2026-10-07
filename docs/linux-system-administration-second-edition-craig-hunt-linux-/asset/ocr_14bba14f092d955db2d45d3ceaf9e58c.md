invaluable in troubleshooting a system. The processes are listed in order from the most resource-intensive to the least intensive, and the display updates itself about every 5 seconds. top reads global configuration information from /etc/toprc and user configuration information from a .toprc file in the user's home directory.

The normal top utility is text-mode, but graphical versions also exist. The graphical versions are available with the GNOME and KDE interfaces. The GNOME version is gtop, or the System Monitor, and the KDE version is ktop, or the Task Manager. As you've seen in previous chapters, we usually don't go for the GUI version of the tool unless it lends itself particularly well to a visual presentation. In the case of table of process information, you'll see that it does. Figure 16.1 shows the standard command-line top utility.

![](bbox=[0.12, 0.25, 0.75, 0.54])

Looking at the sample output, you'll see that the system is running a process called vmware, which is taking up 27.7% of the CPU cycles. It also is using 46.1% of the memory. That's normal; this product is quite resource-intensive and slows down a system quite a bit. Sometimes, however, programs go haywire and start dominating the CPU or the memory and need to be shut down. The top utility will help you find such programs.

Note VMware is a tool for running multiple operating systems on a single computer. An alternative to dual-booting, it provides a virtual machine on an Intel-based computer. This virtual machine is a simulated computer in which an alternative operating system can be installed and run as if it were running on standard PC hardware while actually being isolated from the host's hardware and operating system. For more information, go to the VMware, Inc. site at http://www.vmware.com/.

Other information provided by top includes the process ID (PID), which can be used to kill an errant program; the user who's running the program; the task priority (PRI) and nice value (NI), which determine how Linux allots CPU time to the task; various measures of memory usage (SIZE, RSS, and SHARE); the task's state (STAT)—R for running, S for sleeping, W for swapped out, and so on; and the total CPU time consumed (TIME).

The top utility also has an interactive mode, which allows you to perform tasks like killing a process, changing what information is displayed and how often it is updated, and renicing a process. (We'll talk about renicing a process in the "Tuning the System" section of this chapter.) The

413