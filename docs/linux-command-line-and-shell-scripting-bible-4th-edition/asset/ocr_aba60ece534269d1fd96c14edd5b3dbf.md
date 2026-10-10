+   • **%MEM:** The share of available physical memory the process is using
+   • **TIME+:** The total CPU time the process has used since starting
+   • **COMMAND:** The command-line name of the process (program started)

By default, when you start `top` it sorts the processes based on the %CPU value. You can change the sort order by using one of several interactive commands while `top` is running. Each interactive command is a single character you can press while `top` is running that changes the behavior of the program. Pressing `f` allows you to select the field to use to sort the output, and pressing `d` allows you to change the polling interval. Press `q` to exit the top display. You have lots of control over the output of the top command. Using this tool, you can often find offending processes that have taken over your system. Of course, once you find one, the next job is to stop it, which brings us to the next topic.

# Stopping processes

A crucial part of being a system administrator is knowing when and how to stop a process. Sometimes a process gets hung up and just needs a gentle nudge to either get going again or stop. Other times, a process runs away with the CPU and refuses to give it up. In both cases, you need a command that will allow you to control a process. Linux follows the Unix method of interprocess communication.

In Linux, processes communicate with each other using *signals*. A process signal is a predefined message that processes recognize and may choose to ignore or act on. The developers program how a process handles signals. Most well-written applications have the ability to receive and act on the standard Unix process signals. These signals are shown in Table 4-4.

**TABLE 4-4 Linux Process Signals**

| Signal | Name | Description |
| :--- | :--- | :--- |
| 1 | HUP | Hang up. |