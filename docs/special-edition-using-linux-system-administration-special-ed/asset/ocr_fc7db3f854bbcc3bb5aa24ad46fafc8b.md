kernel needs a module to be loaded, kmod wakes up and spawns a modprobe process that actually loads the module.

kmod offers several advantages over kerneld, including the following:

+   - kmod does not require Sys V IPC support unlike kerneld. This allows Sys V IPC itself to become a module.
+   - Removing kerneld from Sys V IPC made it 40% smaller.
+   - kmod runs as a kernel thread unlike kerneld, which ran as a separate daemon.
+   - kmod reports errors using the normal kernel mechanisms, unlike kerneld which needed Unix domain sockets and thus could not be modularized.

To periodically unload unused modules, you can create a crontab entry for the root user as follows:

```
0-59/5 * * * * /sbin/rmmod -a
```

Add this line to the root user’s crontab file as outlined in Chapter 7, “Scheduling Tasks.”

In order for kmod to be able to spawn modprobe, the kernel must know the path to modprobe. This can be set using the /proc pseudo file system as follows:

```
# echo "/sbin/modprobe" > /proc/sys/kernel/modprobe
```

# UNDERSTANDING THE /proc File System

The /proc file system is a pseudo file system which acts as a window into the internal data structures of the kernel. It can be used to collect information about the kernel and also to modify certain kernel parameters at run time. If you change directory into /proc and do a directory listing, you will find one sub-directory per running process. To get information about a specific process you can list its various attributes, which appear as sub-directories and files within the process directory. Consider the following sample listing of the /proc file system.

```
# ls /proc
1    304   421   441   476   bus        interrupts  misc      slabinfo
2    332   422   460   481   cmdline    ioports     modules   sound
22   355   423   467   482   cpuinfo    kcore       mounts    stat
251  377   424   468   5     devices    kmsg        net       swaps
262  379   425   469   540   dma        ksyms       partitions sys
276  388   426   470   541   filesystems loadavg     pci       tty
290  4     430   471   543   fs         locks       scsi      uptime
3    420   431   472   545   ide        meminfo     self      version
```

To look at information pertaining to the process with PID 1, list the contents of /proc/1:

```
# ls /proc/1
cmdline  cwd  environ  exe  fd  maps  mem  root  stat  statm  status
```

If you want to view the status information for the init process (PID 1), view the contents of /proc/1/status: