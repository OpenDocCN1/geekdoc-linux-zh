
# Starting with Linux Shells

| | | |
|---|---|---|
| 436 ? | SW | 0:00 [httpd] |
| 437 ? | SW | 0:00 [httpd] |
| 438 ? | SW | 0:00 [httpd] |
| 470 ? | S | 0:02 xfs -port -1 |
| 485 ? | S | 0:00 smbd |
| 495 ? | S | 0:00 nmbd -D |
| 533 ? | SW | 0:00 [postmaster] |
| 538 tty1 | SW | 0:00 [minggetty] |
| 539 tty2 | SW | 0:00 [minggetty] |
| 540 tty3 | SW | 0:00 [minggetty] |
| 541 tty4 | SW | 0:00 [minggetty] |
| 542 tty5 | SW | 0:00 [minggetty] |
| 543 tty6 | SW | 0:00 [minggetty] |
| 544 ? | | 0:00 [prefdm] |
| 549 ? | SW | 0:00 [prefdm] |
| 559 ? | | 0:02 [kwm] |
| 585 ? | S | 0:06 kikbd |
| 594 ? | S | 0:00 kmsound |
| 595 ? | S | 0:03 kpanel |
| 596 ? | S | 0:02 kfm |
| 597 ? | S | 0:00 krootwm |
| 598 ? | S | 0:01 kgbgndwm |
| 611 ? | S | 0:00 kmclatop -daemon |
| 666 ? | S | 0:00 /usr/libexec/postfix/master |
| 668 ? | S | 0:00 qmgr -l t-fifo |
| 787 ? | S | 0:00 pickup -l t-fifo |
| 790 ? | S | 0:00 telnetd: 192.168.1.2 [vt100] |
| 791 pts/0 | S | 0:00 login - rich |
| 792 pts/0 | S | 0:00 -bash |
| 805 pts/0 | R | 0:00 ps ax |

The first column in the output shows the process ID (PID) of the process. Notice that the first process is our friend the init process, and assigned PID 1 by the Linux system. All processes that start after the init process are assigned PIDs in numerical order. No two processes can have the same PID.

The third column shows the current status of the process (S for sleeping, SW for sleeping and waiting, and R for running). The process name is shown in the last column. In brackets are processes that have been swapped out of memory to the disk swap space due to inactivity. You can see that some of the processes have been swapped out, but most of the running processes have not.

# Hardware management

Another responsibility for the kernel is hardware management. Any device that the Linux system must communicate with is driver code inserted inside the kernel code. The driver code allows the kernel to pass data back and forth to the device, acting as a middle between applications and the hardware. There are two methods used for inserting driver code in the Linux kernel:

- Drivers compiled in the kernel
- Driver modules added to the kernel

Previously, the only way to insert driver code was to recompile the kernel. Each time you added a new device to the system, you had to recompile the kernel code. This process became even more inefficient as Linux kernels supported more hardware. Fortunately, Linux developers devised a better method to insert driver code into the kernel.

Programmers developed the concept of kernel modules to allow you to insert driver code into a running kernel without having to recompile the kernel. Also, a kernel module could be removed from the kernel when the device was finished being used. This greatly simplified and expanded using hardware with Linux.

The Linux system identifies hardware devices as special files, called device files. There are three different classifications of device files:

- Character
- Block
- Network

Character device files are for devices that can only handle one character at a time. Most types of modems and terminals are created as character files. Block files are for devices that can handle data in large blocks at a time, such as disk drives.

The network files are used for devices that use packets to send and receive data. This includes network cards and a special loopback device that allows the Linux system to communicate with itself using common networking protocols.

Linux creates special files, called nodes, for each device on the system. All communication with the device is performed through the device node. Each node has a unique number pair that identifies it to the Linux kernel. The number pair includes a major and a minor device number. Similar devices are grouped within the same major device group. This is an example of a few device files on a Linux server:

```
$ ls -alda* ttyS*
br-rw-- 1 root disk 8, 0 May 5 2006
br-rw-- 1 root disk 8, 1 May 5 2006 sda1
br-rw-- 1 root disk 8, 10 May 5 2006 sda10
br-rw-- 1 root disk 8, 11 May 5 2006 sda11
br-rw-- 1 root disk 8, 12 May 5 2006 sda12
br-rw-- 1 root disk 8, 13 May 5 2006 sda13
```

# Starting with Linux Shells

```
br-rw-- 1 root disk 8, 14 May 5 2006 sda1
br-rw-- 1 root disk 8, 15 May 5 2006 sda15
br-rw-- 1 root disk 8, 2 May 5 2006 sda2
br-rw-- 1 root disk 8, 3 May 5 2006 sda3
br-rw-- 1 root disk 8, 4 May 5 2006 sda4
br-rw-- 1 root disk 8, 5 May 5 2006 sda5
br-rw-- 1 root disk 8, 6 May 5 2006 sda6
br-rw-- 1 root disk 8, 7 May 5 2006 sda7
br-rw-- 1 root disk 8, 8 May 5 2006 sda8
br-rw-- 1 root disk 8, 9 May 5 2006 sda9
crw---- 1 root tty 4, 64 Jun 29 16 tty0
crw---- 1 root tty 4, 65 May 5 2006 tty1
crw---- 1 root tty 4, 66 May 5 2006 tty2
crw---- 1 root tty 4, 67 May 5 2006 tty3
```

Different Linux handle devices using different names. In fact, the sda device is the first SCSI hard drive, and the tty devices are the standard PC COM ports. The listing shows all of the sda devices that were created on the Linux system. Not all are actually used, but they are created in case the administrator needs them. The fifth column is the device node number. Notice that all of the sda devices have the same major device, 8, while all of the tty devices use 4. The sixth column is the minor device number. Each device within a major number has its own minor device number.

The first column indicates the permissions for the device file. Notice that the SCSI hard drive files are all marked as block (b) device, while the COM port files are marked as character (c) devices.

# Filesystem management

Unlike some operating systems, the Linux kernel can support different types of filesystems to read and write to hard drives. Besides having a dozen filesystems of its own, Linux can read and write to filesystems by other operating systems, such as Microsoft Windows. The kernel must be compiled with support for all types of filesystems that the system will use. Table 1-1 lists the standard filesystems that a Linux system can use to read and write data.

Any hard drive that a Linux server accesses must be formatted using one of the filesystems listed in Table 1-1.

The Linux kernel interfaces with each filesystem using the Virtual File System (VFS). This provides a standard interface for the kernel to communicate with any type of filesystem. VFS caches information in memory as each filesystem is mounted and used.

# Part I The Linux Command Line

| TABLE 1-1 Linux Filesystems |
| Filesystem | Description |
| --- | --- |
| ext | Linux Extended filesystem — the original Linux filesystem |
| ext2 | Second extended filesystem, provided advanced features over ext |
| ext3 | Third extended filesystem, supports journaling |
| hfs | OS/2 high-performance file system |
| jfs | IBM's journaling file system |
| iso9660 | ISO 9660 filesystem (CD-ROMs) |
| minix | MINIX filesystem |
| msdos | Microsoft FAT16 |
| ncp | Network filesystem |
| nfs | Network File System |
| ntfs | Support for Microsoft NT filesystem |
| proc | Access to system information |
| ReiserFS | Advanced Linux file system for better performance and disk recovery |
| smb | Samba SMB filesystem for network access |
| sysv | Older Unix filesystem |
| ufs | Unix-like filesystem that resides on top of MSDOS |
| vfat | Windows 95 filesystem (FAT32) |
| XFS | High-performance 64-bit journaling filesystem |

## The GNU utilities

Besides having a kernel to control hardware devices, a computer operating system needs utilities to perform standard functions, as controlling files and programs. While Linux created the Linux system kernel, he had no system utilities to run it on. Fortunately for him, at the time he was working, a group of people were working together on the Internet to develop a standard set of system utilities that mimicked the Unix operating system.

The GNU organization (GNU stands for GNU's Not Unix) developed a complete set of Unix utilities, but had no kernel system to run them on. These utilities were developed under a software philosophy called open source software (OSS).
