Multiple partitions also make it easier to do certain kinds of backups (such as an image backup). For example, an image backup of /home would be much faster (and probably more useful) than an image backup of the root file system (/).

+   * **Different file system types** — Different kinds of file systems have different structures. File systems of different types must be on their own partitions. In Fedora and RHEL, you need at least one file system type for / (typically ext3) and one for your swap area. File systems on CD-ROM use the iso9660 file system type.

> **TIP:** When you create partitions for Fedora or RHEL, you will often assign the file system type as Linux native (using the ext3 type). Reasons to use other types include needing a file system that allows particularly long filenames or many inodes (each file consumes an inode).
> 
> For example, if you set up a news server, it can use many inodes to store news articles. Another reason for using a different file system type is to copy an image backup tape from another operating system to your local disk (such as one from an OS/2 or Minix operating system).

If you have used only Windows operating systems before, you probably had your whole hard disk assigned to C: and never thought about partitions. With Fedora and RHEL, you can select to have Linux erase the whole disk, take it over, and partition it or have Linux keep separate partitions for Windows 9x/2000/NT/XP/Vista and Linux. The Fedora and RHEL install processes also give you the opportunity to view and change the default partitioning for the different installation types.

During installation, Fedora and RHEL enable you to partition your hard disk using the Disk Setup utility (a graphical partitioning tool). The following sections describe how to use Disk Setup (during installation) or fdisk (when Fedora or RHEL is up and running) or by switching virtual terminals while the install is running). See the section “Tips for creating partitions” for some ideas for creating disk partitions.

# Partitioning with Disk Setup during installation

During installation, you are given the opportunity to change how your hard disk is partitioned. Fedora recommends using the Disk Setup. The Disk Setup screen is divided into two sections. The top shows general information about each hard disk. The bottom shows details of each partition. Figure 2-2 shows an example of the Disk Setup window.

For each of the hard disk partitions, you can see:

+   * **Device** — The device name is the name representing the hard disk partition in the /dev directory. Each disk partition device begins with two letters: sd for IDE disks or SCSI disks, ed for ESDI disks, or xd for XT disks. After that is a single letter representing the number of the disk (disk 1 is a, disk 2 is b, disk 3 is c, and so on). The partition number for that disk (1, 2, 3, and so on) follows that.