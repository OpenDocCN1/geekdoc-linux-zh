+   NI - Nice value, ranging from -20 to +20.

+   SIZE - Total size of the process in kilobytes.

+   RSS - Resident size of the process in kilobytes.

+   STATE - Current state of the process.

+   TIME - Number of system and CPU seconds the process has consumed.

+   %CPU - CPU percentage.

+   %MEM - Memory percentage.

+   COMMAND - Name of the command the process is currently running.

As with most of the commands we have been covering, **top** is different among UNIX variants. You may see some different fields on the different UNIX variants. I am usually confident when I sit down at any UNIX system that I can run **top** and quickly see how the system is running. Most versions of **top** I have run are character-based applications, so you don't even need a graphics terminal to run them. I have run **top** in this example in character mode within an X terminal.

The system used in this example has two CPUs. If you look carefully in the **xosview** window, you'll see that both *CPU0* and *CPU1* are 100 percent used. At the time this screen shot was obtained, I was compiling the Linux kernel on this system, which consumed all the CPU resources on the system for a short period of time. You can see from both the **top** and *System Monitor* windows that the program **cc1**, used to compile the kernel, was consuming a substantial amount of the CPU resources on the system.

Figure 12-3 helps illustrate how different tools can help with viewing how system resources are consumed. **xosview** provides a quick reference, graphical overview of how many system resources are being consumed. **top** and *System Monitor* can be used to determine the specific process consuming the most system resources.