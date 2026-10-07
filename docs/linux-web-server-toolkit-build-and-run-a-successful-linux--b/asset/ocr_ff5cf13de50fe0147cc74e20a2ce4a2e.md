# Chapter 5: Installing Linux

The next installation step is to enter a password for that new user, as follows:

New password for col:
New password (again):

# INSTALLING LILO

One of the final steps of the installation program is to install the Linux boot loader program, LILO. As I stated earlier in this chapter, LILO is a boot manager for Linux that starts the operating system for you and can also start other operating systems on your hard disk.

LILO is a small program that reads a configuration file and gives you options for which operating system should be started. Once you make a choice, it passes control to another program on the hard disk.

The hardest part about using LILO is deciding where to put it. The basic options are follows:

+   **On the Master Boot Record of the first hard disk:** This is the safest way to get Linux to boot, but it is a little dangerous. It can be hard to fix a problem with the Master Boot Record. If the next option works, use it instead.

+   **On the root of the Linux partition:** This enables the Master Boot Record to pass control to LILO without altering that important part of your hard disk. If a problem occurred with the Linux Partition, you could erase the partition and start over, without loosing the entire hard disk.

If you use this option, the Installation utility will mark this as the active partition, so that the MBR will pass control to LILO.

+   **On a floppy disk:** This is a backup system, but you don't really need to do this. The only reason to use a floppy LILO is, for some reason, you don't want to alter the booting sequence of your system in any way. It gives you the most control to booting Linux.

A scenario when this might be appropriate is when you have another operating system such as Windows NT on your computer. Windows NT doesn't work very well as a dual boot with Linux (the previous note). With LILO on a floppy disk, you can just pop the disk in to start your machine when you want to run Linux. This also provides a more secure method; if you don't have the disk, you can't easily start up the machine in Linux.