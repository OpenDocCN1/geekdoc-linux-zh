Linux Runlevels and their Functions

| Runlevel Number | Purpose |
| :--- | :--- |
| 0 | Shuts down the computer |
| 1 | Single user mode |
| 2 | Multi-user mode without Network File System (NFS) support or X |
| 3 | Multi-user mode with NFS support but without X |
| 4 | User-defined |
| 5 | Multi-user mode with NFS support and X |
| 6 | Reboots the computer |

> > **WARNING**
> >
> > Do not use telinit to change to runlevels 0 or 6 unless you intend to shut down or reboot the computer. For these purposes, most administrators prefer to use the shutdown command, as in `shutdown -h now` to shut down or `shutdown -r now` to reboot.

You can switch to runlevel 1 by passing 1 or S as the runlevel number. This runlevel is useful for performing certain types of low-level maintenance and recovery tasks that might be difficult or impossible with regular multiuser services running. For instance, you’re more likely to be able to unmount filesystems for checking, repair, and other changes from single-user mode than from multi-user mode.

# Permanently Changing the Runlevel

When the Linux kernel boots, it launches the init program, which is in charge of handling startup tasks. This program has a PID number of 1 and is at the root of the process tree—all other processes are started by init, either directly or indirectly. To control init, you edit its configuration file, /etc/inittab. This file specifies the default runlevel and provides other options that enable you to control the system startup process.

> > **NOTE**
> >
> > The telinit command is normally a symbolic link to init. On most systems, you can use init instead of telinit to change runlevels, although telinit is the preferred name for this function.