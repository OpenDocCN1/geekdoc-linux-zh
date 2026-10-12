# Disk partitions and sizes

Before Red Hat Linux can be installed, areas of the hard disk are divided up to hold Linux data, swap space, and any other operating systems you may want on your computer. These divisions are called partitions. You can view and change your disk partitions using the fdisk command.

> **CROSS-REFERENCE:** An overview of partitioning is provided in the “Working with File Systems” section of this chapter. Procedures for partitioning your hard disks are explained in Chapter 2.

If you have multiple partitions, you need to watch the percentage of space used on each mounted partition. If, for example, space runs out on a separate /var file system, programs that need to spool data (such as mail and printing utilities), write to log files in /var/log, or use temporary file space in /var/tmp may fail. Even if plenty of space is available in the root partition or another partition, if the assigned partition runs out of space, it won’t draw from other partitions.

More information on monitoring and managing file systems is included later in this chapter.

# Users

User login accounts are listed in the /etc/passwd file. You can list the contents of this file to see what users have accounts on your Linux system as follows:

```
# less /etc/passwd
```

Administrative logins (up to UID 100 in the third colon-separated field) should make up most of the first few entries in this file. Regular user accounts (with UIDs above 100) are usually added in after the administrative accounts.

As an administrator of a multiuser Red Hat Linux system, you need to make sure that user accounts are kept up to date. To keep your Red Hat Linux system secure, you need to remove users when they leave your organization (or at least deactivate their passwords if their home directories still contain information that your organization needs).

> **CROSS-REFERENCE:** Chapter 11 contains information on how to set up and manage users in Linux.

# The kernel

The heart of the Linux system is called the kernel. The kernel provides the interface between you (and the programs you run) and the hardware (hard disks, RAM, network cards, etc.). Using the /proc file system, you can find out a lot of information about your kernel, by simply displaying the contents of /proc files.

For each process currently running in Linux, there is a directory in /proc consisting of the process number for the running process. (Type ps aux | more to see the running processes