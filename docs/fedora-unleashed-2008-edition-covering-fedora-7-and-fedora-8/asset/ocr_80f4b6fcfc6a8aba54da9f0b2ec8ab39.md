Next, the BIOS looks on the bootable volume for boot code in the partition boot sector also known as the Master Boot Record (MBR) of the first hard disk. The MBR contains the boot loader code and the partition table—think of it as an index for a book, plus a few comments on how to start reading the book. (We cover the MBR in more detail in Chapter 35, "Managing the File System.") If the BIOS finds a boot loader, it loads the boot loader code into memory. At that point, the BIOS's job is completed, and it passes control of the system to the boot loader.

The boot loader locates the Linux kernel on the disk and loads it into memory. After that task is completed, the boot loader passes control of the system to the Linux kernel. You can see how one process builds on another in an approach that enables many different operating systems to work with the same hardware.

Fedora can use a variety of boot loaders, including GRUB (the default for Fedora), LILO (a long-time standard but not available with Fedora), BootMagic (a commercial program), and others.

# NOTE

Linux is very flexible and can be booted from multiple images on a CD-ROM, over a network using PXE (pronounced “pixie”) or NetBoot, or on a headless server with the console display sent over a serial or network connection. Work is under way to create a special Linux BIOS at http://www.linixbios.org/ that expedites the boot process because Linux does not need many of the services offered by the typical BIOS.

This kind of flexibility enables Linux to be used in a variety of ways, such as remote servers or diskless workstations, which are not generally seen in personal home use.

# Loading the Linux Kernel

In a general sense, the kernel manages the system resources. As the user, you do not often interact with the kernel, but instead just the applications that you are using. Unix refers to each application as a process, and the kernel assigns each process a number called a process ID (PID). First, the Linux kernel loads and runs a process named init, which is also known as the “father of all processes” because it starts every subsequent process. The init process looks for a list of instructions in a file named /etc/rc.d/rc.sysinit. That script issues a number of commands that are run only once—each time the system is turned on.

# NOTE

Details about the sequence of events that occur when the Linux kernel is loaded can be found in the file /usr/src/linux-2.6/init/main.c if you installed the Linux kernel documentation.

This next step of the boot process begins with a message that the Linux kernel is loading, and a series of messages is printed to the screen, giving you the status of each command