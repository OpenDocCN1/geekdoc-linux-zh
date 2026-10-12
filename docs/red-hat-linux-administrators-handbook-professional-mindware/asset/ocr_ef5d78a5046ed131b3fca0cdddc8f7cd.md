# # Chapter 2

# ## Boot Up and Shutdown Configuration

# ### Configuring the Very First Process: init

A Red Hat Linux kernel (that is, the core operating system) is typically stored in a compressed file. When the kernel is started by a boot loader program, such as LILO, it uncompresses itself, initializes the display device, and starts checking for other hardware attached to your computer. As it finds your hard disks, floppy drives, network cards, and so forth, it loads the appropriate device driver modules. During this process, it displays text messages on your console screen.

At this point, the kernel mounts the root file system (/) as read-only and performs checks on the file system. If the kernel finds that everything is okay, it mounts the root file system as read/write. If a problem arises and the kernel fails to mount the root partition, the kernel panics and the system halts. If the disk somehow was corrupt, the kernel might provide an option to run a file system checker program, such as fsck.ext2, from a restricted shell. In such a case, run fsck.ext2 on the root partition or any other partition that failed during boot. For example, if your system's root partition resides on /dev/sda1 (a SCSI disk partition) and it fails, run

```
fsck.ext2 /dev/sda1
```