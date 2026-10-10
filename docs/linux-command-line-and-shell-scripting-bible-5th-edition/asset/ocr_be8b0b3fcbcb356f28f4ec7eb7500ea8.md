# Chapter 1: Starting with Linux Shells

This same concept is still in place with the Linux kernel code, except that instead of just Linus controlling the kernel code, a team of developers has taken on the task.

The kernel is primarily responsible for four main functions:

+   - System memory management
+   - Software program management
+   - Hardware management
+   - Filesystem management

The following sections explore each of these functions in more detail.

# System memory management

One of the primary functions of the operating system kernel is memory management. Not only does the kernel manage the physical memory available on the server, but it can also create and manage *virtual memory*, or memory that does not actually exist.

It does this by using space on the hard disk, called the *swap space*. The kernel swaps the contents of virtual memory locations back and forth from the swap space to the actual physical memory. This allows the system to think there is more memory available than what physically exists.

# Software program management

The Linux operating system calls a running program a *process*. A process can run in the *foreground*, displaying output on a display, or it can run in *background*, behind the scenes. The kernel controls how the Linux system manages all the processes running on the system.

The kernel creates the first process, called the *init process*, to start all other processes on the system. When the kernel starts, it loads the init process into virtual memory. As the kernel starts each additional process, it gives the process a unique area in virtual memory to store the data and code that the process uses.

A few different types of init process implementations are available in Linux, but these days the two most popular are

+   - **SysVinit:** The *SysVinit (SysV)* initialization method, the original method used by Linux, was based on the UNIX System V initialization method. Although it is not used by many Linux distributions these days, you still may find it around in older Linux distributions.
+   - **Systemd:** The *systemd* initialization method, created in 2010, has become the most popular initialization and process management system used by Linux distributions.

> **NOTE**  
> In Chapter 4, “More Bash Shell Commands,” you see how to use the `ps` command to view the processes currently running on the Linux system.