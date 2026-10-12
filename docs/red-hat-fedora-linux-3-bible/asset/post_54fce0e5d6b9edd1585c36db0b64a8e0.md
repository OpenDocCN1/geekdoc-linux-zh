
![](img/b22364e57409c2481ba806e4e6b9309c_78_0.png)

If you have only used Windows operating systems before, you probably had your whole hard disk assigned to C: and never thought about partitions. With Fedora Core, you can do a Server class of install (and have Linux erase the whole disk, take it over, and partition it) or a Personal Desktop or Workstation class (and have Linux keep separate partitions for Windows 9x/2000/NT/XP and Linux). With the latest version of Fedora Core, you also have the opportunity to view and change the default partitioning for the different installation types.

During installation, Fedora enables you to partition your hard disk using the Disk Druid utility (a graphical partitioning tool). The following sections describe how to use Disk Druid (during installation) or fdisk (when Fedora is up and running). See the section “Tips for creating partitions” for some ideas for creating disk partitions.

## Partitioning with Disk Druid during installation

During installation, you are given the opportunity to change how your hard disk is partitioned. Fedora recommends using the Disk Druid. The Disk Druid screen is divided into two sections. The top shows general information about each hard disk. The bottom shows details of each partition. Figure 2-2 shows an example of the Disk Druid window.

For each of the hard disk partitions, you can see:

- **Device** — The device name is the name representing the hard disk partition in the /dev directory. Each disk partition device begins with two letters: hd for IDE disks, sd for SCSI disks, ed for ESDI disks, or xd for XT disks. After that is a single letter representing the number of the disk (disk 1 is a, disk 2 is b, disk 3 is c, and so on). The partition number for that disk (1, 2, 3, and so on) follows that.
- **Mount Point/Raid/Volume** — The directory where the partition is connected into the Linux file system (if it is). You must assign the root partition ( / ) to a native Linux partition before you can proceed. If you are using RAID or LVM, the name of the RAID device or LVM volume appears here.
- **Type** — The type of file system that is installed on the disk partition. In most cases, the file system will be Linux (ext3), Win VFAT (vfat), or Linux swap. However, you can also use the previous Linux file system (ext2), physical volume (LVM), or software RAID.

![](img/b22364e57409c2481ba806e4e6b9309c_79_0.png)

Figure 2-2: Partition your disk during installation from the Disk Setup window.

- **Format** — Indicates whether (check mark) or not (no check mark) the installation process should format the hard disk partition. Partitions marked with a check are erased! So, on a multi-boot system, be sure your Windows partitions, as well as other partitions containing data are not checked!
- **Size (MB)** — The amount of disk space allocated for the partition. If you selected to let the partition grow to fill the existing space, this number may be much larger than the requested amount.
- **Start/End** — Represents the partition’s starting and ending cylinders on the hard disk.

In the top section, you can see each of the hard disks that are connected to your computer. The drive name is shown first. The Geometry section (Geom) shows the numbers of cylinders, heads, and sectors, respectively, on the disk. That’s followed by the model name of the disk. The total amount of disk space, the amount used, and the amount free are shown in megabytes.

## Reasons for partitioning

There are different opinions about how to divide up a hard disk. Here are some issues:

- **Do you want to install another operating system?** If you want Windows on your computer along with Linux, you will need at least one Windows (Win95 FAT16, VFAT, or NTFS type), one Linux (Linux ext3), and one Linux swap partition.
- **Is it a multiuser system?** If you are using the system yourself, you probably don’t need many partitions. One reason for partitioning an operating system is to keep the entire system from running out of disk space at once. That also serves to put boundaries on what an individual can use up in his or her home directory (although disk quotas are good for that as well).
- **Do you have multiple hard disks?** You need at least one partition per hard disk. If your system has two hard disks, you may assign one to / and one to /home (if you have lots of users) or /var (if the computer is a server sharing lots of data).

## Deleting, adding, and editing partitions

Before you can add a partition, there needs to be some free space available on your hard disk. If all space on your hard disk is currently assigned to one partition (as it often is in DOS or Windows), you must delete or resize that partition before you can claim space on another partition. The section on reclaiming disk space discusses how to add a partition without losing information in your existing single-partition system.

> **CAUTION:** Make sure that any data that you want to keep is backed up before you delete the partition. When you delete a partition, all its data is gone.

Disk Druid is less flexible, but more intuitive, than the fdisk utility. Disk Druid lets you delete, add, and edit partitions.

> **TIP:** If you create multiple partitions, make sure that there is enough room in the right places to complete the installation. For example, most of the Linux software is installed in the /usr directory (and subdirectories), whereas most user data are eventually added to the /home or /var directories.

To delete a partition in Disk Druid, do the following:

1.  Select a partition from the list of Current Disk Partitions on the main Disk Druid window (click it or use the arrow keys).
2.  To delete the partition, click **Delete**.
3.  When asked to confirm the deletion, click **Delete**.
4.  If you made a mistake, click **Reset** to return to the partitioning as it was when you started Disk Druid.

To add a partition in Disk Druid, follow these steps from the main Disk Druid window:

1.  Select **New**. A window appears, enabling you to create a new partition.
2.  Type the name of the **Mount Point** (the directory where this partition will connect to the Linux file system). You need at least a root (/) partition and a swap partition.
3.  Select the **type of file system** to be used on the partition. You can select from Linux native (ext2 or preferably ext3), software RAID, Linux swap (swap), physical volume (LVM), or Windows FAT (vfat).

> TIP: To create a different file system type than those shown, leave the space you want to use free for now. After installation is complete, use `fdisk` to create a partition of the type you want.

4.  Type the number of megabytes to be used for the partition (in the **Size** field). If you want this partition to grow to fill the rest of the hard disk, you can put any number in this field (I will do 1f).
5.  If you have more than one hard disk, select the disk on which you want to put the partition from the **Allowable Drives** box.
6.  Type the size of the partition (in megabytes) into the **Size (MB)** box.
7.  Select one of the following **Additional Size Options**:
    - **Fixed size** — Click here to use only the number of megabytes you entered into the Size text box when you create the partition.
    - **Fill all space up to (MB)** — If you want to use all remaining space up to a certain number of megabytes, click here and fill in the number. (You may want to do this if you are creating a VFAT partition up to the 2048MB limit that Disk Druid can create.)
    - **Fill to maximum allowable size** — If you want this partition to grow to fill the rest of the disk, click here.
8.  Optionally select **Force to Be a Primary Partition** if you want to be sure to be able to boot the partition or **Check for Bad Blocks** if you want to have the partition checked for errors.
9.  Select **OK** if everything is correct. (The changes don’t take effect until several steps later when you are asked to begin installing the packages.)

To edit a partition in Disk Druid from the main Disk Druid window, follow these steps:

1.  Click the partition you want to edit.
2.  Click the **Edit** button. A window appears, ready to let you edit the partition definition.
3.  Change any of the attributes (as described in the add partition procedure). For a new install, you may need to add the mount point (/ ) for your primary Linux partition.
4.  Select **OK**. (The changes don’t take effect until several steps later, when you are asked to begin installing the packages.)

> NOTE: If you want to create a RAID device, you need to first create at least two RAID partitions. Then click the **RAID** button to make the two partitions into a RAID device. For more information on RAID, refer to Chapter 10 or the Red Hat Linux Customization guide. The latter is available from any Red Hat mirror site (such as `ftp.redhat.com`), here: `pub/redhat/current/en/doc/RH-DOCS/rhl-cg-en-9/*`. To create an LVM volume group, you must create at least one partition of type “physical volume (LVM).”
