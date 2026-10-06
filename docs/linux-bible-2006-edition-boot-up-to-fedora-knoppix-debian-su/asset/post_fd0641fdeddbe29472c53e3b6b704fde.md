
## Part III ♦ Choosing and Installing a Linux Distribution

If you have used only Windows systems before, you probably never thought about partitions. the whole hard disk assigned to C:. With many Linux systems, you have the opportunity to view and change the default partitioning based on how you want to use the system.

During installation, systems such as SUSE and Fedora let you partition your hard disk using graphical partitioning tools (Yast and Disk Druid, respectively). The following sections describe how to use Disk Druid (during installation) or fdisk. The section "Tips for Creating Partitions" provides some ideas for creating disk partitions.

## Partitioning with Disk Druid Installation

During installation, Fedora gives you the opportunity to change how your hard disk is partitioned using a tool called Disk Druid. The Disk Druid screen is divided into two sections. The top shows general information about each hard disk. The bottom shows details of each partition. Figure 7-1 shows an example of the Disk Druid window.

![](img/a2d958d7eab32ca5b89b2b8af808aa70_285_0.png)

Figure 7-1: Partition your disk during Fedora installation from the Disk Setup window.

For each of the hard partitions, you can see:

- **Device** — The device name is what represents the hard partition in the /dev directory. Each partition device begins with two letters: hd for IDE disks, sd for SCSI disks, or rd for SCSI disks. After that is a single letter representing the number of the disk (disk 1 is a, disk 2 is b, disk 3 is c, and so on). The partition number for disk (1, 2, 3, and so on) follows that. For example, /dev/hda1 represents the first partition on the first IDE hard on the computer.
- **Mount Point/Read/Volume** — The directory where the partition is connected into the Linux file system (if it is). You must assign the root partition (/) to a native Linux partition before you proceed. If you are using RAID or LVM, the name of the RAID device or LVM volume appears here.
- **Type** — The type of file system that is installed on the disk. In many cases, the file system will be Linux (ext3), FAT (vfat), or Linux swap. You can also use Linux file system (ext2), physical volume (LVM), or software RAID.
- **Format** — Indicates whether (check mark) or (no check mark) the installation process should format the hard disk. Partitions marked with a check are erased! On multiuser system, partitions containing data are not checked.
- **Size (MB)** — The amount of disk space allocated for the partition. If you select to fill the existing space, this number may be much larger than the requested amount.
- **Start/End** — Represents the partition's starting and ending cylinders on the hard disk. In the top section, you can see each of the hard disks connected to your computer. The drive name is shown first. The Geometry section shows the numbers of cylinders, heads, and sectors, respectively. That is followed by the name of the disk. The total amount of disk space, the amount used, and the amount free are in megabytes.

## Reasons for Partitioning

There are different opinions about how to divide up hard disk. Here are some issues:

- **Do you want to install another operating system?** If you want Windows on your computer along with Linux, you will need at least one partition (Windows95, VFAT, or NTFS type), one Linux (ext3), and one Linux swap.
- **Is it a multiuser system?** If you are using the same system, reason for partitioning is to keep the entire system from running out of disk space at once. also serves to put boundaries on what an individual can use.
- **Do you have multiple hard disks?** You need at least one partition per hard disk. If your system has two hard disks, you may assign one to / and one to /home or /var.

## Deleting, Adding, and Editing Partitions

Before you add a partition, there needs to be some free space available on hard disk. If all space on your hard disk is currently assigned to one partition (as in DOS), you must delete or resize that partition before you can claim space on another. "Dual Booting with Linux" discusses how to add a partition without losing information in your existing system. When you delete a partition, all its data is gone.

Disk Druid is less flexible but more intuitive than the fdisk utility. It lets you add and edit partitions. If you create multiple partitions, make sure there is enough room in the right places to complete the installation. For example, most of Linux is installed in the /usr directory (and subdirectories), whereas most user data are eventually added to /home or /var directories.

To delete a partition in Disk Druid, do the following:

1. Select a partition from the list on the main Druid window (click it or use the arrow keys).
2. To delete the partition, click Delete.
3. When asked to confirm the deletion, click Delete.
4. If you make a mistake, click Reset to return to partitioning as it was when you started Disk Druid.

To add a partition in Disk Druid, follow these steps from the main Druid window:

1. Select New. A window appears, enabling you to create a new partition.
2. Type the Mount Point (the directory where this partition will connect to the Linux file system). You need at least a root (/) and a swap partition.
3. Select the type of file system to be used on the partition. You can select from Linux (ext2 or ext3), software RAID, Linux swap, physical volume (LVM), or FAT (vfat). To create a system type different from those shown, leave the space you want to use free for now. After installation is complete, fdisk to create a partition of the type you want.
4. Type the number of megabytes to be used for the partition (in the Size field). If you want this partition to grow to fill the rest of the hard disk, you can put any number in this field (1 will do fine).
5. If you have more than one hard disk, select the disk on which you want to put the partition from the allowable Drives box.
6. Type the size of the partition (in megabytes) into the Size (MB) box.
7. Select one of the following Additional Size Options:
    - **Fixed size** — Click here to use only the number of megabytes entered into the Size box when you create the partition.
    - **Fill all space up to (MB)** — If you want to use all remaining space up to a certain number of megabytes, click here and fill in the number (You may want to do this if you are creating a VFAT partition up to the 2048MB limit that Disk Druid can create).
    - **Fill to maximum allowable size** — If you want this partition to grow to fill the rest of the disk, click here.
8. Optionally select Force to Be a Primary Partition if you want to boot the partition or Check for Bad Blocks if you want to have the partition checked for errors.
9. Select OK if everything is correct. (The changes don't take effect until several steps later when you are asked to begin installing the packages.)

To edit a partition in Disk Druid from the main Druid window, follow these steps:

1. Click the partition you want to edit.
2. Click the Edit button. A window appears, ready to let you edit the partition definition.
3. Change any of the attributes (as described in the add partition procedure). For a new install, you may need to add the mount point (/) for your primary Linux partition.
4. Select OK. (The changes don't take effect until several steps later when you are asked to begin installing the packages.)

### Partitioning with fdisk

The fdisk utility is available with every Linux system for creating and working with disk partitions in Linux. It does the same job as graphical partitioning tools such as Disk Druid, although it's no longer offered as an option for Fedora installation. However, during Fedora installation, and other Linux installations that have virtual terminals running, you can switch to a shell (press Ctrl+Alt+F2) and use fdisk manually to partition your hard disk.
