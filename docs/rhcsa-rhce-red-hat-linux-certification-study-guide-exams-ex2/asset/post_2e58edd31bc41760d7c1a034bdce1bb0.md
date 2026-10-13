
- 6. Repeat Steps 3 and 4. What's the difference in the output to the mount command?
- 7. Run the tune2fs -O extent,uninit_bg,dir_index /dev/sda1 command. Do you see a message in the output?
- 8. Apply the fsck.ext4 command on the partition. What do you see?
- 9. Repeat Step 6.
- 10. Now on the other partition created in Exercise 6-1, apply the mkfs.ext4 /dev/sdb1 command.
- 11. Mount the newly formatted partition on the /net directory, and run the mount command by itself. Can you confirm the format of the /dev/sdb1 partition?

## CERTIFICATION OBJECTIVE 6.03

## Basic Linux Filesystems and Directories

Everything in Linux can be reduced to a file. Partitions are associated with filesystem device nodes such as /dev/sda1. Hardware components are associated with node files such as /dev/dvd. Detected devices are documented as files in the /proc directory. The Filesystem Hierarchy Standard (FHS) is the official way to organize files in Unix and Linux directories. As with the other sections, this introduction provides only the most basic overview of the FHS. More information is available from the official FHS home page at www.pathname.com/fhs.

## Separate Linux Filesystems

There are several major directories associated with all modern Unix/Linux operating systems. Files, drivers, kernels, logs, programs, utilities, and more are organized in these directories. The way these components are organized on storage media is known as a filesystem. It's based on the way the filesystem is formatted, and the directory where that filesystem is mounted. The FHS makes it easier for users of other Unix-based operating systems to understand the basics of Linux.

Every FHS starts with the top-level root directory, also known by its symbol, the single forward slash (/). All of the other directories shown in Table 6-4 are subdirectories of the root directory. Unless mounted separately, you can also find their files on the same partition as the root directory. You may not see some of the directories shown in the table if associated packages have not been installed. Not all directories shown are officially part of the FHS. More important, not all listed directories can or should be mounted separately.

Mounted directories are often known as volumes, which can span multiple partitions. However, while the root directory (/) is the top-level directory in the FHS, the root user's home directory (/root) is just a subdirectory.

![](img/9139201cfcaf4292284a0eed074928e5_353_0.png)

> In Linux, the word filesystem has several different meanings. For example, a filesystem can refer to the FHS, an individual volume, or a format such as ext3. A filesystem device node such as /dev/sda1 represents the partition on which a directory can be mounted.

## Directories That Can Be Mounted Separately

If space is available, several directories listed in Table 6-4 are excellent candidates to be mounted separately. As discussed in Chapter 1, it's typical to mount directories such as /, /boot, /home, /opt, /srv, /tmp, and /var on separate volumes. Sometimes, it makes sense to mount lower-level subdirectories on separate volumes, such as /var/ftp for an FTP server or /var/www for a Web server.

But first, several directories should always be maintained as part of the top-level root directory filesystem. These directories include: /bin, /dev, /etc, /lib, /root, /sbin, and /selinux. Files within these directories are essential to the smooth operation of Linux as an operating system. While the same argument can be made for the /boot directory, it is a special case. The storage of the Linux kernel, Initial RAM Disk, and bootloader files in this directory can help protect the core of the operating system when there are other problems.

This ignores directories with virtual filesystems, including /proc and /sys. Files in these directories are filled only during the boot process and disappear when a system is shut down. As there's nothing to store from these directories, there's no reason to mount them separately. Some directories listed in Table 6-4 are designed for use only as mount points. In other words, they should normally be empty. If you store files on those directories, they won't be accessible if, say, a network share is mounted on them. Typical network mount points include the /media, /mnt, /net, and /smb directories.

## TABLE 6-4 Basic Filesystem Hierarchy Standard Directories

| Directory | Description |
|---|---|
| / | The root directory, the top-level directory in the FHS. All other directories are subdirectories of root, which is always mounted on some volume. |
| /bin | Essential command line utilities. Should not be mounted separately; otherwise, it could be difficult to get to these utilities when using a rescue disk. |
| /boot | Includes Linux startup files, including the Linux kernel. The default, 500MB, is usually sufficient for a typical modular kernel and additional kernels that you might install during the RHCE or RHCSA exam. |
| /dev | Hardware and software device drivers for everything from floppy drives to terminals. Do not mount this directory on a separate volume. |
| /etc | Most basic configuration files. Do not mount this directory on a separate volume. |
| /home | Home directories for almost every user. |
| /lib | Program libraries for the kernel and various command line utilities. Do not mount this directory on a separate volume. |
| /media | The mount point for removable media, including floppy drives, DVDs, and Zip disks. |
| /misc | The standard mount point for local directories mounted via the automounter. |
| /mnt | A legacy mount point; formerly used for removable media. |
| /net | The standard mount point for network directories mounted via the automounter. |
| /opt | Common location for third-party application files. |
| /proc | Currently running kernel-related processes, including device assignments such as IRQ ports, I/O addresses, and DMA channels, as well as kernel configuration settings such as IP forwarding. As a virtual filesystem, Linux automatically configures it as a separate filesystem in RAM. |
| /root | The home directory of the root user. Do not mount this directory on a separate volume. |
| /sbin | System administration commands. Don't mount this directory separately. |
| /selinux | Currently configured settings associated with Security Enhanced Linux. Do not mount this directory on a separate volume. |
| /smb | The standard mount point for remote shared Microsoft network directories mounted via the automounter. |
| /srv | Commonly used by various network servers on non-Red Hat distributions. |
| /tftpboot | Included if the TFTP server is installed. |
| /tmp | Temporary files. By default, Red Hat Enterprise Linux deletes all files in this directory periodically. |
| /usr | Small programs accessible to all users. Includes many system administration commands and utilities. |
| /var | Variable data, including log files and printer spools. |

## CERTIFICATION OBJECTIVE 6.04

## Logical Volume Management (LVM)

Logical Volume Management (LVM, also known as the Logical Volume Manager) can allow you to manage the space allocated to appropriate directories. As an example, assume the /var and /home directories are configured on separate logical volumes. If extra space is available on the volume associated with the /var directory, you can reallocate space to the volume associated with the /home directory. Alternatively, if you are managing a server on a growing network, new users will be common. Periodically, more room may be needed on a volume associated with the /home directory. With LVM, you can add a new physical disk and allocate its storage capacity to an existing /home directory volume.

![](img/9139201cfcaf4292284a0eed074928e5_355_0.png)

> While LVM can be an important tool to manage the space available to different volumes, it does not provide redundancy. However, you can use LVM in concert with a RAID array.

## Definitions in LVM

To work with LVM, you need to understand how partitions configured for that purpose are used. First, with the fdisk and parted utilities, you need to create partitions configured to the LVM partition type. The commands within those utilities were described earlier in this chapter.

Once those partitions are available, they need to be set up as physical volumes (PVs). That process sets up the physical partitions into manageable chunks known as physical extents (PEs). With the right commands, you can then convert those PEs to logical extents (LEs). Those LEs can be organized into logical volumes (LVs). You can then create volume groups (VGs) from part or all of an LV. That VG can then be formatted and mounted on an appropriate directory. For those who are new to LVM, it may be important to break out each definition:

- Physical volume (PV) A PV is a partition, configured to the LVM partition type.
- Physical extent (PE) A PE is a small uniform segment of disk space. PVs are split into PEs.
