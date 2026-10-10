
Figure 10.1: Content of the root directory (SUSE)

```bash
$ cd /
$ ls -l
insgesamt 125

drwxr-xr-x   2 root root   4096 Dez 20 12:37 bin
drwxr-xr-x   2 root root   4096 Jan 27 13:19 boot
lrwxrwxrwx   1 root root     17 Dez 20 12:51 cdrecord -> /media/cdrecorder
lrwxrwxrwx   1 root root     12 Dez 20 12:51 cdrom -> /media/cdrom
drwxr-xr-x  27 root root  49152 Mär  4 07:49 dev
drwxr-xr-x  40 root root   4096 Mär  4 09:16 etc
lrwxrwxrwx   1 root root     13 Dez 20 12:51 floppy -> /media/floppy
drwxr-xr-x   6 root root   4096 Dez 20 16:28 home
drwxr-xr-x   6 root root   4096 Dez 20 12:36 lib
drwxr-xr-x   6 root root   4096 Feb  2 12:43 media
drwxr-xr-x   2 root root   4096 Mär 21 2002 mnt
drwxr-xr-x  14 root root   4096 Mär  3 12:54 opt
dr-xr-xr-x  95 root root      0 Mär  4 08:49 proc
drwx------  11 root root   4096 Mär  3 16:09 root
drwxr-xr-x   4 root root   4096 Dez 20 13:09 sbin
drwxr-xr-x   6 root root   4096 Dez 20 12:36 srv
drwxrwxrwt  23 root root   4096 Mär  4 10:45 tmp
drwxr-xr-x  13 root root   4096 Dez 20 12:55 usr
drwxr-xr-x  17 root root   4096 Dez 20 13:02 var
```

There is considerable consensus about the FHS, but it is just as “binding” as anything on Linux, i.e., not that much. On the one hand, those certainly are Linux systems (for example the one on your broadband router or PVR) that are mostly touched only by the manufacturer and where conforming to every nook and cranny of the FHS does not gain anything. On the other hand, you may do whatever you like on your own system, but must be prepared to bear the consequences—your distributor assures you to keep to his side of the FHS bargain, but also expects you not to complain if you are not playing completely by the rules and problems do occur. For example, if you install a program in /usr/bin and the file in question gets overwritten during the next system upgrade, this is your own fault since, according to the FHS, you are not supposed to put your own programs into /usr/bin (/usr/local/bin would have been correct).

## The Operating System Kernel—/boot

The /boot directory contains the actual operating system: vmlinuz is the Linux kernel. In the /boot directory there are also other files required for the boot loader (LILO or GRUB).

## General Utilities—/bin

In /bin there are the most important executable programs (mostly system programs) which are necessary for the system to boot. This includes, for example, mount and mkdir. Many of these programs are so essential that they are needed not just during system startup, but also when the system is running—like ls and grep. /bin also contains programs that are necessary to get a damaged system running again if only the file system containing the root directory is available. Additional programs that are not required on boot or for system repair can be found in /usr/bin.

## Special System Programs—/sbin

Like /bin, /sbin contains programs that are necessary to boot or repair the system. However, for the most part these are system configuration tools that can really be used only by root. “Normal” users can use some of these programs to query the system, but can’t change anything. As with /bin, there is a directory called /usr/sbin containing more system programs.

## System Libraries—/lib

This is where the “shared libraries” used by programs in /bin and /sbin reside, as files and (symbolic) links. Shared libraries are pieces of code that are used by various programs. Such libraries save a lot of resources, since many processes use the same basic parts, and these basic parts must then be loaded into memory only once; in addition, it is easier to fix bugs in such libraries when they are in the system just once and all programs fetch the code in question from one central file. Incidentally, below /lib/modules there are **kernel modules**, i.e., kernel code which is not necessarily in use—device drivers, file systems, or network protocols. These modules can be loaded by the kernel when they are needed, and in many cases also be removed after use.

## Device Files—/dev

This directory and its subdirectories contain a plethora of entries for device files. **Device files** form the interface between the shell (or, generally, the part of the system that is accessible to command-line users or programmers) and the device drivers inside the kernel. They have no “content” like other files, but refer to a driver within the kernel via “device numbers”.

In former times it was common for Linux distributions to include an entry in /dev for every conceivable device. So even a laptop Linux system included the device files required for ten hard disks with 63 partitions each, eight ISDN adapters, sixteen serial and four parallel interfaces, and so on. Today the trend is away from overfull /dev directories with one entry for every imaginable device and towards systems more closely tied to the running kernel, which only contain entries for devices that actually exist. The magic word in this context is udev (short for userspace /dev) and will be discussed in more detail in *Linux Administration I*.

Linux distinguishes between **character devices** and **block devices**. A character device is, for instance, a terminal, a mouse or a modem—a device that provides or processes single characters. A block device treats data in blocks—this includes hard disks or floppy disks, where bytes cannot be read singly but only in groups of 512 (or some such). Depending on their flavour, device files are labelled in “ls -l” output with a “c” or “b”:

```bash
crw-rw- -   1 root root  10,   4 Oct 16 11:11 amigamous
brw-rw- ---   1 root disk   8,   1 Oct 16 11:11 sda1
brw-rw- ---   1 root disk   8,   2 Oct 16 11:11 sda2
crw-rw- -   1 root root   1,   3 Oct 16 11:11 null
```

Instead of the file length, the list contains two numbers. The first is the “major device number” specifying the device’s type and governing which kernel driver is in charge of this device. For example, all SCSI hard disks have major device number 8. The second number is the “minor device number”. This is used by the driver to distinguish between different similar or related devices or to denote the various partitions of a disk.

There are several notable **pseudo devices**. The **null device**, /dev/null, is like a “dust bin” for program output that is not actually required, but must be directed somewhere. With a command like

```bash
$ program >/dev/null
```

the program’s standard output, which would otherwise be displayed on the terminal, is discarded. If /dev/null is read, it pretends to be an empty file and returns end-of-file at once. /dev/null must be accessible to all users for reading and writing.

The “devices” /dev/random and /dev/urandom return random bytes of “crypto-graphic quality” that are created from “noise” in the system—such as intervals between unpredictable events like key presses. Data from /dev/random is suitable for creating keys for common cryptographic algorithms. The /dev/zero file returns an unlimited supply of null bytes; you can use these, for example, to create or overwrite files with the dd command.

## The /etc Directory

The /etc directory is very important; it contains the configuration files for most programs. Files /etc/inittab and /etc/init.d/*, for example, contain most of the system-specific data required to start system services. Here is a more detailed description of the most important files—except for a few of them, only user root has write permission but everyone may read them.

- **/etc/fstab**
  This describes all mountable file systems and their properties (type, access method, “mount point”).

- **/etc/hosts**
  This file is one of the configuration files of the TCP/IP network. It maps the names of network hosts to their IP addresses. In small networks and on freestanding hosts this can replace a name server.

- **/etc/inittab**
  The /etc/inittab file is the configuration file for the init program and thus for the system start.

- **/etc/init.d/\***
  This directory contains the “init scripts” for various system services. These are used to start up or shut down system services when the system is booted or switched off.

![](img/44bdd771e9c9b1353d2401c2892b2459_137_0.png)

- **/etc/issue**
  This file contains the greeting that is output before a user is asked to log in. After the installation of a new system this frequently contains the name of the vendor.

- **/etc/motd**
  This file contains the “message of the day” that appears after a user has successfully logged in. The system administrator can use this file to notify users of important facts and events[^1].

- **/etc/mtab**
  This is a list of all mounted file systems including their mount points. /etc/mtab differs from /etc/fstab in that it contains all currently mounted file systems, while /etc/fstab contains only settings and options for file systems that might be mounted—typically on system boot but also later. Even that list is not exhaustive, since you can mount file systems via the command line where and how you like.

![](img/44bdd771e9c9b1353d2401c2892b2459_137_1.png)

- **/etc/passwd**
  In /etc/passwd there is a list of all users that are known to the system, together with various items of user-specific information. In spite of the name of the file, on modern systems the passwords are not stored in this file but in another one called /etc/shadow. Unlike /etc/passwd, that file is not readable by normal users.

[^1]: There is a well-known claim that the only thing all Unix systems in the world have in common is the “message of the day” asking users to remove unwanted files since all the disks are 98% full.

## The /opt Directory

This directory is really intended for third-party software—complete packages prepared by vendors that are supposed to be installable without conflicting with distribution files or locally-installed files. Such software packages occupy a subdirectory /opt/(package). By rights, the /opt directory should be completely empty after a distribution has been installed on an empty disk.
