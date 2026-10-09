# Table 3–3
Available file systems.

| File System Type | Description |
| :--- | :--- |
| ext2 | An older native Linux file system type. |
| ext3 | The newest native Linux file system and an enhanced version of ext2. This is the default type. |
| physical volume (LVM) | Allows dynamic sizing of logical volumes within a group volume. |
| software RAID | Implements the various RAID levels in the kernel. This is an inexpensive implementation of RAID, allowing the use of IDE and SCSI hard drives. |
| swap | Swap space is used in Linux when the amount of physical memory is full. Swap should be twice your computer's RAM, but not larger than 2 GB. |
| vfat | This file system type is compatible with Windows systems. |

remaining space as one large volume for everything else. This is a great way to just avoid the issue altogether.

After you have used the system, you can determine the sizes of the partitions more easily, but to change the sizes now requires backing up the data, repartitioning, formatting the new partition, and then restoring the data. The **physical volume (LVM)** file system type allows you to create a single volume group and logical volumes to hold the /, /usr, and /home file systems. If the /home file system fills up, you can shrink the /usr file system and then increase /home.

When you are finished modifying the disk partitions, select OK to continue the installation.

![](bbox=[0.21, 0.52, 0.3, 0.57])

# Installing a Boot Loader

A boot loader is the first software program that runs when a computer starts. It loads and then transfers control to the operating system kernel software. The kernel then initializes the rest of the operating system. You can use a floppy disk as a boot loader, or you can use a boot loader located on the hard disk. Red Hat Linux comes with two boot loader programs, GRUB and LILO.

Grand Unified Bootloader (GRUB) was originally designed and implemented by Eric Stefan Bolen. It is now managed by GNU. GRUB is a multiboot boot loader, meaning that it supports multiple operating systems. This is useful if you have more than one operating system loaded on your hard drive (called dual boot). GRUB is the default boot loader for Red Hat Linux installation.

Linux Loader (LILO) is an older loader program and is the most widely used. LILO is a versatile boot loader for Linux. It does not depend on a specific file system. It can boot the Linux kernel images from floppy disk and hard disk, and can even boot other operating systems. Up to sixteen different images can be selected at boot time.

You can select GRUB, LILO, or no boot loader. If you select no boot loader, then you must have a floppy disk or an existing boot loader to load your Linux operating system. You have an opportunity to create a boot floppy at the end of the installation process.

Select the GRUB boot loader, shown in Figure 3–12, for your installation. It really doesn't matter which boot loader you use, but you will use GRUB throughout the remainder of this book.

There are options that you can identify for the boot loader to pass to the Linux kernel to use at boot time. These are discussed in a later chapter. You have an opportunity to enter boot parameters during every Linux startup, so you do not have to enter values at this time. We are not going to pass any values to the kernel at this time.

The **Force use of LBA32 (not normally required)** option, shown in Figure 3–13, allows you to exceed the 1024-cylinder limit for the /boot partition. If you have a system that supports the LBA32 extension for booting operating systems above the 1024-cylinder limit,