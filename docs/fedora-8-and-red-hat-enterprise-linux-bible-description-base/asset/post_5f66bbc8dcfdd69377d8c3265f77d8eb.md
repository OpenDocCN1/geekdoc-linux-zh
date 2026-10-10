
## Using Windows partitions from Linux

With some space available on your disk, when you go to install Linux, consider adding a small FAT16 or FAT32 partition (maybe 2GB) on your disk. Every x86 operating system (Linux, Windows 95, NT, 2000, XP and DOS) supports those types. With that added, you will be able to freely exchange files between your Linux and Windows system on the FAT16 partition.

With FAT partitions, however, keep in mind that there are limitations. FAT is limited to between 2GB and 4GB file sizes. Also, FAT16 doesn't support long file names. Total partition size for FAT file systems is 32GB.

After you have installed Linux in the space freed up by the previous procedure, you should be able to choose between Linux and Windows when the Fedora or RHEL boot screen appears during boot time. Press any key to go to the GRUB boot screen. Then move the arrow key to choose to boot Linux or Windows.

The first time you boot Windows, you might be asked to check your disk (because your Windows partition will be a different size than expected). After that, there should be no change in how you use your Windows system. Your disk space will just be smaller.

![](img/fb202c163797a743c3c6cf236316bc96_98_0.png)

> **NOTE:** By default, Fedora and RHEL are configured to hide the GRUB boot screen that lets you select which operating system to boot. You will have to press Enter as the Fedora boot screen counts down 5 seconds to see the GRUB boot screen. You might consider editing the grub.conf file, as described later in this chapter. Personally, I removed the hiddenmenu line and increased the timeout from 5 to 10 seconds.

Now, when you boot up Linux, if you have a lot of documents, digital images, music, or other content on your Windows partition, you probably want to be able to use that content from Linux. To do that, you need to:

- Determine which partition is your Windows partition.
- If you didn't do so during installation, add support for the file system type of your Windows partition to Linux. Since VFAT is already built in, that means adding NTFS support if that is the file system type.
- Mount the Windows partition on your Linux file system.

The following procedure describes how to do those things.

**1. Check partitions.** To determine which partition contains your Windows file system, use the `fdisk` command as follows:

```
# fdisk -l
Disk /dev/sda: 60.0 GB, 60011642880 bytes
16 heads, 63 sectors/track, 116280 cylinders
Units = cylinders of 1008 * 512 = 516096 bytes

Device Boot Start End Blocks Id System
/dev/sda1 * 1 41725 21029053+ 7 HPFS/NTFS
/dev/sda2 106741 116280 4808160 12 Compaq diagnostics
/dev/sda3 41725 41932 104422+ 83 Linux
/dev/sda4 41932 106734 32660145 5 Extended
/dev/sda5 41932 106718 32652081 8e Linux LVM
```

In this example, the Windows partition is on device /dev/sda1 and is an NTFS file system. (The other common type of Windows file system is VFAT.)

**2. Get NTFS support.** If you have a VFAT file system, you can skip this step. If you have an NTFS file system, and NTFS support is not already installed, you can install the necessary drivers and tools to be able to mount and use your NTFS file system in Linux by running the following yum command as root user from a Terminal window:

```
# yum install ntfsprogs ntfs-3g
```

Assuming you have an active connection to the Internet, this will install the NTFS support you need to access your NTFS partitions from Linux.

**3. Mount Windows file system.** You can access your Windows file system from Linux using the mount command. Assuming your Windows partition is an NTFS file system on /dev/sda1 (as in the example above), you could type the following to create the Windows mount point and mount the file system there:

```
# mkdir /mnt/win
# chmod 755 /mnt/win
# mount -o ro -t ntfs /dev/sda1 /mnt/win
# chmod 755 /mnt/win
# ls /mnt/win
```

The `-o ro` option to mount will mount the file system read-only. Read/write support is not considered to be stable (so if you remove the `-o ro` option to mount read/write, you do so at your own risk). Replace the `ntfs` with `vfat` if your Windows partition is a VFAT file system. The `ls` command is just to find out if you can see the contents of your Windows partition.

You can have the mount occur permanently by adding an entry to the `/etc/fstab` file. Here's an example of the line you could add to `/etc/fstab` to have the partition mounted every time the system reboots:

```
/dev/sda1 /mnt/win ntfs ro 0 0
```

At this point, you can use the files from your Windows partition as you would any other files on your system. You can open a folder or change directories to the `/mnt/win` directory to see the contents. Then use any applications you choose to open your documents (OpenOffice.org), music (Rhythmbox), images (gimp), or any other content type you want to use from your Windows partition in Linux.

> **NOTE:** If your Linux system uses an ext2 or ext3 file system (as Fedora typically does), you can do the reverse of what was just described as well: access your Linux partition from Windows. For information on how to do this, see The Ext2 Installable File System for Windows (www.fs-driver.org).

## Partitioning your disks

The hard disk (or disks) on your computer provides the permanent storage area for your data files, applications programs, and the operating system (such as Fedora or RHEL). Partitioning is the act of dividing a disk into logical areas that can be worked with separately. There are several reasons you may want to do partitioning:

- **Multiple operating systems** — If you install Fedora or RHEL on a PC that already has a Windows operating system, you may want to keep both operating systems on the computer. To run efficiently, they must exist on completely separate partitions. When your computer boots, you can choose which system to run. Note that you are limited in the number of partitions you can have (with IDE drives you can have 63 partitions; with SCSI devices, you are limited to 15 partitions per device).

- **Multiple partitions within an operating system** — To protect from having their entire operating system run out of disk space, people often assign separate partitions to different areas of the Linux file system. For example, if `/home` and `/var` were assigned to separate partitions, then a gluttonous user who fills up `/home` partition wouldn't prevent logging daemons from continuing to write to log files in the `/var/log` directory.

Multiple partitions also make it easier to do certain kinds of backups (such as an image backup). For example, an image backup of /home would be much faster (and probably more useful) than an image backup of the root file system (/).

- **Different file system types** — Different kinds of file systems have different structures. File systems of different types must be on their own partitions. In Fedora and RHEL, you need at least one file system type for / (typically ext3) and one for your swap area. File systems on CD-ROM use the iso9660 file system type.

> **TIP:** When you create partitions for Fedora or RHEL, you will often assign the file system type as Linux native (using the ext3 type). Reasons to use other types include needing a file system that allows particularly long filenames or many inodes (each file consumes an inode).
> 
> For example, if you set up a news server, it can use many inodes to store news articles. Another reason for using a different file system type is to copy an image backup tape from another operating system to your local disk (such as one from an OS/2 or Minix operating system).

If you have used only Windows operating systems before, you probably had your whole hard disk assigned to C: and never thought about partitions. With Fedora and RHEL, you can select to have Linux erase the whole disk, take it over, and partition it or have Linux keep separate partitions for Windows 9x/2000/NT/XP/Vista and Linux. The Fedora and RHEL install processes also give you the opportunity to view and change the default partitioning for the different installation types.

During installation, Fedora and RHEL enable you to partition your hard disk using the Disk Setup utility (a graphical partitioning tool). The following sections describe how to use Disk Setup (during installation) or fdisk (when Fedora or RHEL is up and running) or by switching virtual terminals while the install is running. See the section “Tips for creating partitions” for some ideas for creating disk partitions.

## Partitioning with Disk Setup during installation

During installation, you are given the opportunity to change how your hard disk is partitioned. Fedora recommends using the Disk Setup. The Disk Setup screen is divided into two sections. The top shows general information about each hard disk. The bottom shows details of each partition. Figure 2-2 shows an example of the Disk Setup window.

For each of the hard disk partitions, you can see:

- **Device** — The device name is the name representing the hard disk partition in the /dev directory. Each disk partition device begins with two letters: sd for IDE disks or SCSI disks, ed for ESDI disks, or xd for XT disks. After that is a single letter representing the number of the disk (disk 1 is a, disk 2 is b, disk 3 is c, and so on). The partition number for that disk (1, 2, 3, and so on) follows that.
