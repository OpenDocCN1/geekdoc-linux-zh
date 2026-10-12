# Using the top Utility

To view the top CPU processes — the ones that use most of the CPU time — you can use the top program. To start that program, select Main Menu Programs Utilities Top from the GNOME desktop or type top in a terminal window (or text console). The top program then displays a text screen listing the current processes, arranged in descending order of CPU usage, along with various other information such as memory and swap space usage. Figure 28-1 shows a typical output from the top program.

![](bbox=[0.22, 0.35, 0.7, 0.57])

Figure 28-1
Viewing top CPU processes

The top utility updates the display every five seconds. You can keep top running in a window so that you can continually monitor the status of your Red Hat Linux system. You quit top by pressing Ctrl+C or by closing the terminal window.

The first five lines of the output screen provide summary information about the system. Here is what these five lines show:

+   1. The first line shows the current time, how long the system has been up, how many users are logged in, and three load averages (the average number of processes ready to run during the last 1, 5, and 15 minutes).
+   2. The second line lists the total number of processes and the status of these processes.
+   3. The third line shows CPU usage — what percentage of CPU time user processes employ, what percentage system (kernel) processes use, and what percentage of time the CPU is idle.