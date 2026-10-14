# CHAPTER SUMMARY

+   - Linux is a multiprocessing operating system. Each process is managed by the Linux kernel, which can allocate resources to a process and end a process if necessary. CPU time is allocated in time slices.
+   - New processes are created by forking an existing process. Processes in Linux have parent-child relationships.
+   - The state of each process is tracked by the kernel and can be viewed using command-line or graphical utilities. If a process is not active, the kernel can move part of its data to swap space, which acts as virtual memory to allow more processes to be managed at the same time.
+   - Multiple processes can be started from a single shell. Starting a process with an ampersand runs the program in the background.
+   - Within a shell, the jobs command manages multiple processes started in that shell. You can also place jobs in the foreground or background using the fg and bg commands.
+   - Virtual consoles let you log in at multiple independent text-mode screens.
+   - The ps command can display many different fields of information about each process, as determined by command-line options, including parent-child relationships between processes. You can also select which processes to display using command-line options.
+   - The kill command sends signals to processes or to the Linux kernel when necessary to end a process.
+   - You can view process information within the /proc file system or using a number of utilities, such as ps and top.
+   - Each process in Linux is assigned a priority, called a nice level. You can raise the nice level to make a process run slower (be nicer to other processes). The root user can change the priority of any process; other users can raise the nice level of processes they have started.
+   - The nice and renice commands set a process's nice level; other command-line and graphical programs also let you change a process's nice level.
+   - The top command lists processes according to how much CPU time they are using. The output of top is updated every few seconds. top can also be used to control processes by sending them signals.
+   - KDE System Guard and the GNOME System Monitor are two useful graphical process management utilities. Each displays many fields of information about each process and can be used to send signals to a process.
+   - Many system administrators like to display a CPU load monitor on the Panel of their desktop so they can keep an eye on system load.
+   - Shared libraries let many Linux programs access the same programming functionality without loading it into memory multiple times.