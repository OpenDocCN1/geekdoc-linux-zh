# # CHAPTER 12
## System-Monitoring Tools

T To keep your system in optimum shape, you need to keep a close eye on it. Such monitoring is imperative in a corporate environment where uptime is vital and any system failures can cost real money. Whether it is checking processes for any errant daemons or keeping a close eye on CPU and memory use, Fedora provides a wealth of utilities designed to give you as little or as much feedback as you want. This chapter looks at some of the basic monitoring tools, along with some tactics designed to keep your system up longer. Some of the monitoring tools cover network connectivity, memory, and hard drive use, but all should find a place in your sysadmin toolkit. Finally, you will learn how to manipulate active system processes, using a mixture of graphical and command-line tools.

# ## Console-Based Monitoring

Those familiar with UNIX system administration already know about the ps or process display command commonly found on most flavors of UNIX. Because Linux is closely related to UNIX, it also benefits from this command and allows you to quickly see the current running processes on the system, as well as who owns them and how resource hungry they are.

Although the Linux kernel has its own distinct architecture and memory management, it also benefits from enhanced use of the /proc file system, the virtual file system found on many UNIX flavors. Through the /proc file system, you can communicate directly with the kernel to get a deep view of what is currently happening. Developers tend to use the /proc file system as a way of getting information

# IN THIS CHAPTER

+   - Console-Based Monitoring
+   - Using the kill Command to Control Processes
+   - Using Priority Scheduling and Control
+   - Displaying Free and Used Memory with free
+   - Graphical Process and System Management Tools
+   - KDE Process- and System- Monitoring Tools
+   - Reference