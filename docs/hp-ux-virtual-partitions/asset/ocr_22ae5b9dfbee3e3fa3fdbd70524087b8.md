# **TABLE 3-5 hpxux Examples**

**Command** (all at ISL> prompt) **Comments**

Automatic Boot **hpxux** No interaction - autoboot sequence.

**hpxux -s** Bring up system at run level s for single-user mode.

**hpxux** Default boot sequence from *autoexecute* normally object file is /stand/vmunix.

**hpxux vmunix.test** Boot object file *vmlnux.test*.

**hpxux (5.2,5.0.0) /stand/vmunix** Boot from /stand/vmunix on the disk at the path 52.5.0.0.

**hpxux lan(32) /stand/vmunix** Boot from LAN.

**hpxux -v** Get HP-UX version numbers.

**hp-ux ll /stand** List contents of /stand on root disk.

![](bbox=[0.06, 0.39, 0.14, 0.49])

The part of the boot that takes place after the **hpxux** command is issued is in the four following parts:

+   1.  HP-UX initializes the system hardware and devices - The HP-UX kernel locates and initializes system hardware such as memory, I/O busses and devices, and so on. Kernel device drivers are associated with I/O devices at this time. You see many messages fly-by on the system console as this process is taking place.
+   2.  HP-UX kernel data structures are created and initialized - There are many tables for system processes and memory, file systems, and so on, that are created. You also see the status of this part of the boot on the system console.
+   3.  HP-UX searches for the root file system - The base file system contains critical system files and is usually found on the disk from which HP-UX boots. Many commands are run as part of this process.
+   4.  HP-UX starts the init process called /sbin/init - The init process, which has an ID of one, starts all other processes on the system. The init process reads /etc/inittab for direction. There is a detailed description of the contents of /etc/inittab in Chapter 7.