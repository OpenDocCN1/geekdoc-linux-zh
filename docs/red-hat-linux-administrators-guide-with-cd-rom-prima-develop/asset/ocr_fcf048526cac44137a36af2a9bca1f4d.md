With Linux, you can identify and track every process that is running on your system. A *process* is a single program running in its own virtual space on the operating system. It is separate from a job or command, which can be several distinct processes working in tandem to complete a specific task. Each individual command is executed as a single process. A process has a wide range of uses and can be one of many things: anything from a daemon to an application currently running on the display, or a system program executing a planned or needed function. Linux assigns to each of these processes a number that can then be used to change the process's function or state. Manipulating a process's attributes grants the user more freedom in determining how Linux operates and what type of priority each program is given. Sending commands to the processes themselves also grants both the user and the system a large amount of flexibility in tailoring the system's operation.

This chapter will cover the following topics:

+   - Process ID numbers
+   - ID numbers assigned to users and groups
+   - The priority and nice value of processes
+   - The life cycle of a process
+   - The commands and signals used to manipulate a process

# ## Understanding Processes

Linux is extremely dynamic in how it allows users to track each and every program running on the system. Along with the ability to view each and every process, administrators can also change the manner in which it operates. Individual processes can be stopped, started, killed and modified. Nearly every function or operation executed under Linux can be monitored. With that monitoring comes the ability to change the program's priority or to kill it altogether. Though users should leave many operations alone—such as those that the system requires in order to run—others, especially those initiated by normal users on the system, can be customized.