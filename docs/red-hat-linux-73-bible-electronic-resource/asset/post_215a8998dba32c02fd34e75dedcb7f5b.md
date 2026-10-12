
The `%post` command starts the post-installation section. After it, you can add any shell commands you want to run after installation is completed. By default, you should have useradd commands for users you added during installation.

### Commands To Be Run Post-Installation

```text
%post
/usr/sbin/useradd jake
chfn -f 'John W. Jones' jake
/usr/sbin/usermod -p '$I$ake' k
```

At this point you should have a working ks.cfg file.

# Installing the kickstart file

Once the ks.cfg file is created, you need to put it somewhere accessible to the computer doing the installation. Typically, you will place the file on a floppy disk. However, you can also put the file on a computer that is reachable on the network or on a hard disk.

To copy the file to a floppy disk, create a DOS floppy and copy the file as follows:

```text
# mcopy ks.cfg a:
```

When you do the Red Hat Linux kickstart installation, you must have this floppy disk with you.

Being able to place the ks.cfg file on a computer on the network requires a bit more configuration. The network must have a DHCP or a BOOTP server configured that is set up to provide network information to the new install computer. The NFS server containing the ks.cfg file must export the file so that it is accessible to the computer installing Linux. To use a ks.cfg file from the local hard disk, you can place the file on any partition that is a Windows (VFAT) or Linux (ext3) partition.

# Booting a kickstart installation

If the kickstart file (ks.cfg) has been created and installed in an accessible location, you can start the kickstart installation. Here is an example of how you can do a kickstart installation using the Red Hat Linux CD and a floppy containing a ks.cfg file:

- 1. Insert the Red Hat Linux CD and restart the computer.
- 2. When you see the boot prompt, insert the floppy containing the ks.cfg file and type the following (quickly, before the installation boots on its own):

```text
boot: linux ks=file:/fd0/ks.cfg
```

You should see messages about formatting the file system and reading the package list. The packages should install, with the only intervention required being to change CDs. Next you should see a post-install message. Finally, you should see the "Complete" message.

- 3. Remove the floppy; then press the Spacebar to restart your computer (the CD should eject automatically).

> TIP: To fully automate the kickstart process, you need to do a hard disk or network install. You can install using kickstart over NFS (*ks:nfs:server:path*), from a Web server (*ks=http://server/path*), or from your hard drive (*ks=hd:device*).

# Special Installation Topics

Some things that you run into during installation merit whole discussions by themselves. Rather than bog down the procedures with details that not everyone needs, I have added these topics to this section. Descriptions expand on things such as reclaiming disk space, partitioning, and other topics, such as reconfiguring your kernel.

## Partitioning your disks

The hard disk (or disks) on your computer provides the permanent storage area for your data files, applications programs, and the operating system (such as Red Hat Linux). Partitioning is the act of dividing a disk into logical areas that can be worked with separately. There are several reasons you may want to do partitioning:

- **Multiple operating systems** — If you install Red Hat Linux on a PC that already has a Windows operating system, you may want to keep both operating systems on the computer. To run efficiently, they must exist on completely separate partitions. When your computer boots, you can choose which system to run.
- **Multiple partitions within an operating system** — To protect from having your entire operating system run out of disk space, people often assign separate partitions to different areas of the Red Hat Linux file system. For example, if `/home` and `/var` were assigned to separate partitions, then a gluttonous user who fills up the `/home` partition wouldn't prevent logging daemons from continuing to write to log files in the `/var/log` directory.

Multiple partitions also make it easier to do certain kinds of backups (such as an image backup). For example, an image backup of /home would be much faster (and probably more useful) than an image backup of the root file system (/).

- **Different file system types** — Different kinds of file systems that have different structures. File systems of different types must be on their own partitions. In Red Hat Linux, you need at least one file system type for / (typically ext3) and one for your swap area. File systems on CD-ROM use the iso9660 file system type.

> TIP: When you create partitions for Red Hat Linux, you will usually assign the file system type as Linux native (using the ext3 type). Reasons to use other types include needing a file system that allows particularly long filenames or many inodes (each file consumes an inode).

> For example, if you set up a news server, it can use many inodes to store news articles. Another reason for using a different file system type is to copy an image backup tape from another operating system to your local disk (such as one from an OS/2 or Minix operating system).

If you have only used Windows operating systems before, you probably had your whole hard disk assigned to C: and never thought about partitions. With Red Hat Linux, you can do a Server class of install (and have Linux erase the whole disk, take it over, and partition it) or a Workstation class (and have Linux keep separate partitions for Windows 9x/2000 and Linux). With the latest version of Red Hat Linux, you also have the opportunity to view and change the default partitioning for the different installation types.

During installation, Red Hat enables you to partition your hard disk using either the Disk Druid (a graphical partitioning tool) or the fdisk utility (a text-based partitioning tool). The following sections describe those and other related tools. See the section "Tips for creating partitions" for some ideas for creating disk partitions.

## Partitioning with Disk Druid during installation

During a custom installation, you are given the opportunity to change how your hard disk is partitioned. Red Hat recommends using the Disk Druid. Figure 2-1 is an example of the Disk Druid screen from the Red Hat Linux Installation Guide.

![](img/1744bde8c889adfab3fc911e1687fecf_64_0.png)

**Figure 2-1:** Change disk partitions during installation using Disk Druid.

The Disk Druid screen is divided into two sections. The top shows general information about each hard disk and primary partition. The bottom shows details of each partition.

For each of the hard disk partitions, you can see:

- **Device** — The device name is the name representing the hard disk partition in the `/dev` directory. Each disk partition device begins with two letters: hd for IDE disks, sd for SCSI disks, ed for ESDI disks, or xd for XT disks. After that is a single letter representing the number of the disk (disk 1 is a, disk 2 is b, disk 3 is c, and so on). The partition number for that disk (1, 2, 3, and so on) follows that.
- **Start/End** — Represents the partition's starting and ending cylinders on the hard disk.
- **Size (MB)** — The amount of disk space actually allocated for the partition. If you selected to let the partition grow to fill the existing space, this number may be much larger than the requested amount.
- **Type** — The type of file system that is installed on the disk partition. In most cases, the file system will be Linux (ext3), Win 95 FAT16 (fat), Win VFAT (vfat), or Linux swap. Table 2-1 lists the types of file systems that are available to assign to a disk partition. The number associated with each type of file system is what you would actually type if you were to assign that file system to a partition.

> **NOTE:** Not all file system types are supported in Red Hat Linux. Of those that are, some are not built into the kernel by default (such as NTFS). Even fewer are available to be created in Disk Druid. To see which file systems are built into the kernel, type `cat /proc/filesystems`. Accessing other file system types may require you to load the module using the `insmod` command (for example, `insmod minix`). Most of your needs should be served by `ext3` (Linux), `fat` and `vfat` (DOS/Windows), `swap` (Linux swap), and `iso9660` (CD-ROM). Those are all loaded automatically as they are needed.

- **Mount Point** — The directory where the partition is connected into the Linux file system (if it is). You must assign the root partition (`/`) to a native Linux partition before you can proceed.
- **Format** — Indicates whether (Yes) or not (No) the installation process should format the hard disk partition. Partitions marked `Yes` are erased! So, on a multiboot system, be sure to mark your Windows partitions, as well as other partitions containing data you want to keep, `No`!

## Table 2-1: File System Types and Numbers for Disk Partition

| Number | File System Type | Number | File System Type | Number | File System Type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 01 | FAT12 | 42 | SFS | 87 | NTFS volume set |
| 02 | XENIX root | 4D | QNX4.x | 93 | Amoebe |
| 03 | XENIX usr | 4E | QNX4.x 2nd part | 94 | Amoebe BBT |
| 04 | FAT16 <32M | 4F | QNX4.x 3rd part | A0 | IBM Thinkpad hiberna |
