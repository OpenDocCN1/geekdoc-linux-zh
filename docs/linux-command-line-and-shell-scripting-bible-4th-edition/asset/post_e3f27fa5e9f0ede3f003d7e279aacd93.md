
## System Runlevels and Initialization

The following table lists standard system runlevels:

| Runlevel | Description |
|---|---|
| 2 | Multi-user mode without networking services enabled |
| 3 | Multi-user mode with networking services enabled |
| 4 | Custom |
| 5 | Multi-user mode with GUI available |
| 6 | Reboot the system |

The /etc/inittab file defines the default runlevel for a system. The processes that start for specific runlevels are defined in subdirectories of the /etc/rc.d directory. You can view the current runlevel at any time using the runlevel command:

```bash
$ runlevel
N 5
$
```

The systemd initialization method became popular because it has the ability to start processes based on different events:

- When the system boots
- When a particular hardware device is connected
- When a service is started
- When a network connection is established
- When a timer has expired

The systemd method determines what processes to run by linking events to unit files. Each unit file defines the programs to start when the specified event occurs. The systemctl program allows you to start, stop, and list the unit files currently running on the system.

The systemd method groups unit files together into targets. A target defines a specific running state of the Linux system, similar to the SysVinit runlevel concept. At system startup, the default.target unit defines all the unit files to start. You can view the current default target using the systemctl command:

```bash
$ systemctl get-default
graphical.target
$
```

The graphical target unit file defines the processes to start when a multi-user graphical environment is running, similar to the old SysVinit runlevel 5.

> **NOTE** In *Chapter 4*, “More Bash Shell Commands,” you'll see how to use the `ps` command to view the processes currently running on the Linux system.

## Hardware management

Still another responsibility for the kernel is hardware management. Any device that the Linux system must communicate with needs driver code inserted inside the kernel code. The driver code allows the kernel to pass data back and forth to the device, acting as an intermediary between applications and the hardware. Two methods are used for inserting device driver code in the Linux kernel:

- Drivers compiled in the kernel
- Driver modules added to the kernel

Previously, the only way to insert device driver code was to recompile the kernel. Each time you added a new device to the system, you had to recompile the kernel code. This process became even more inefficient as Linux kernels supported more hardware. Fortunately, Linux developers devised a better method to insert driver code into the running kernel.

Programmers developed the concept of kernel modules to allow you to insert driver code into a running kernel without having to recompile the kernel. Also, a kernel module could be removed from the kernel when the device was finished being used. This greatly simplified and expanded using hardware with Linux.

The Linux system identifies hardware devices as special files, called *device files*. There are three classifications of device files:

- Character
- Block
- Network

Character device files are for devices that can handle data only one character at a time. Most types of modems and terminals are created as character files. Block files are for devices that can handle data in large blocks at a time, such as disk drives.

The network file types are used for devices that use packets to send and receive data. This includes network cards and a special loopback device that allows the Linux system to communicate with itself using common network programming protocols.

Linux creates special files, called nodes, for each device on the system. All communication with the device is performed through the device node. Each node has a unique number pair that identifies it to the Linux kernel. The number pair includes a major and a minor device number. Similar devices are grouped into the same major device number. The minor device number is used to identify a specific device within the major device group.

## Filesystem management

Unlike some other operating systems, the Linux kernel can support different types of filesystems to read and write data to and from hard drives. Besides having over a dozen filesystems of its own, Linux can read and write to and from filesystems used by other operating systems, such as Microsoft Windows. The kernel must be compiled with support for all types of filesystems that the system will use. Table 1-2 lists the standard filesystems that a Linux system can use to read and write data.

### TABLE 1-2 Linux Filesystems

| Filesystem | Description |
|---|---|
| ext | Linux extended filesystem—the original Linux filesystem |
| ext2 | Second extended filesystem; provided advanced features over ext |
| ext3 | Third extended filesystem; supports journaling |
| ext4 | Fourth extended filesystem; supports advanced journaling |
| btrfs | A newer, high-performance filesystem that supports journaling and large files |
| exfat | The extended Windows filesystem, used mainly for SD cards and USB sticks |
| hpfs | OS/2 high-performance filesystem |
| jfs | IBM's journaling filesystem |
| iso9660 | ISO 9660 filesystem (CD-ROMs) |
| minix | MINIX filesystem |
| msdos | Microsoft FAT16 |
| ncp | NetWare filesystem |
| nfs | Network File System |
| ntfs | Support for Microsoft NT filesystem |
| proc | Access to system information |
| smb | Samba SMB filesystem for network access |
| sysv | Older Unix filesystem |
| ufs | BSD filesystem |
| umsdos | Unix-like filesystem that resides on top of msdos |
| vfat | Windows 95 filesystem (FAT32) |
| XFS | High-performance 64-bit journaling filesystem |

Any hard drive that a Linux server accesses must be formatted using one of the filesystem types listed in Table 1-2.

The Linux kernel interfaces with each filesystem using the Virtual File System (VFS). This provides a standard interface for the kernel to communicate with any type of filesystem. VFS caches information in memory as each filesystem is mounted and used.

## The GNU utilities

Besides having a kernel to control hardware devices, a computer operating system needs utilities to perform standard functions, such as controlling files and programs. Although Linus created the Linux system kernel, he had no system utilities to run on it. Fortunately for him, at the same time he was working, a group of people were working together on the Internet trying to develop a standard set of computer system utilities that mimicked the popular Unix operating system.

The GNU organization (GNU stands for GNU’s Not Unix) developed a complete set of Unix utilities but had no kernel system to run them on. These utilities were developed under a software philosophy called open source software (OSS).

The concept of OSS allows programmers to develop software and then release it to the world with no licensing fees attached. Anyone can use, modify, or incorporate the software into their own system without having to pay a license fee. Uniting Linus’s Linux kernel with the GNU operating system utilities created a complete, functional, free operating system.

Although the bundling of the Linux kernel and GNU utilities is often just called Linux, you will see some Linux purists on the Internet refer to it as the GNU/Linux system to give credit to the GNU organization for its contributions to the cause.

## The core GNU utilities

The GNU project was mainly designed for Unix system administrators to have a Unix-like environment available. This focus resulted in the project porting many common Unix system command-line utilities. The core bundle of utilities supplied for Linux systems is called the *coreutils* package.

The GNU coreutils package consists of three parts:

- Utilities for handling files
- Utilities for manipulating text
- Utilities for managing processes

Each of these three main groups of utilities contains several utility programs that are invaluable to the Linux system administrator and programmer. This book covers each of the utilities contained in the GNU coreutils package in detail.

## The shell

The GNU/Linux shell is a special interactive utility. It provides a way for users to start programs, manage files on the filesystem, and manage processes running on the Linux system. The core of the shell is the command prompt. The command prompt is the interactive part of the shell. It allows you to enter text commands, and then it interprets the commands and executes them in the kernel.

The shell contains a set of internal commands that you use to control tasks such as copying files, moving files, renaming files, displaying the programs currently running on the system, and stopping programs running on the system. Besides the internal commands, the shell allows you to enter the name of a program at the command prompt. The shell passes the program name off to the kernel to start it.

You can also group shell commands into files to execute as a program. Those files are called *shell scripts*. Any command that you can execute from the command line can be placed in a shell script and run as a group of commands. This provides great flexibility in creating utilities for commonly run commands or processes that require several commands grouped together.

Quite a few Linux shells are available to use on a Linux system. Different shells have different characteristics, some being more useful for creating scripts and some being more useful for managing processes. The default shell used in all Linux distributions is the Bash shell. The Bash shell was developed by the GNU project as a replacement for the standard Unix shell, called the Bourne shell (after its creator). The Bash shell name is a play on this wording, referred to as the “Bourne again shell.”

In addition to the Bash shell, we will cover several other popular shells in this book. Table 1-3 lists the different shells we will examine.
