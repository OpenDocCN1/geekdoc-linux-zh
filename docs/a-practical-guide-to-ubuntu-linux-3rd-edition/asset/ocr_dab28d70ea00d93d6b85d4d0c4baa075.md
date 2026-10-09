init daemon As the last step of the boot procedure, Linux starts the Upstart **init daemon** (page 432) as PID number 1. The **init** daemon is the first gennnne process to run after booting and is the parent of all system processes. (Which is why when you kill process 1 while you are working with **root** privileges, the system dies.)

Once **init** is running, the startup event triggers the **rc-sysinit** task, which stops when the system enters any runlevel. The **rc-sysinit** task executes **telinit** with the argument specified by **DEFAULT_RUNLEVEL** in the **rc-sysinit.conf** file. See page 439 for more information.

Reinstalling the MBR If the master boot record (MBR) is overwritten, the system will not boot into Linux and you need to rewrite the MBR. See page 589 for details.

# ## RECOVERY (SINGLE-USER) MODE

When the system is in recovery (single-user) mode, only the system console is enabled. You can run programs from the console in recovery mode just as you would from any terminal in multiuser mode with three differences: You cannot run graphical programs (because you are working in textual mode), few of the system daemons are running, and all filesystems are mounted as specified by `/etc/fstab` (page 510), but they are mounted *readonly*. You can use the **mount remount** and **rw** options to enable write access to a filesystem (page 222).

# ### Ubuntu uses the term recovery mode, not single-user mode

> What was classically called *single-user mode*. Ubuntu refers to as *recovery mode*. However, some vestiges of the old terminology remain. For example, you type **single** at the end of the GRUB linux line to bring a system up in recovery mode. This book uses these terms interchangeably.

When you boot the system to recovery mode, the Upstart **init** daemon runs the job named **rc5** (`/etc/init/rc5.conf`) as part of recovery mode initialization (see the caution on page 444). See the next sections for instructions on booting a system to recovery mode. When you bring a running system down to recovery mode (page 451), the Upstart **init** daemon runs jobs named **rc** (`/etc/init/rc.conf`) and **rc5**.

With the system in recovery mode, you can perform system maintenance that requires filesystems to be unmounted or that requires just a quiet system—no one except you using it, so that no user programs interfere with disk maintenance and backup programs. The classical UNIX term for this state is *quiescent*. You can often boot to recovery mode when the system will not boot normally, allowing you to change or replace configuration files, check and repair partitions using **fsck** (page 512), rewrite boot information (page 589), and more.

# ### BOOTING THE SYSTEM TO RECOVERY (SINGLE-USER) MODE

You can bring a system up to recovery mode by booting from the hard disk and giving GRUB the appropriate instructions.

Displaying the GRUB menu The first step in bringing a system up in recovery mode from the hard disk is to display the GRUB menu (Figure 11-1, next page). Boot the system normally (turn on