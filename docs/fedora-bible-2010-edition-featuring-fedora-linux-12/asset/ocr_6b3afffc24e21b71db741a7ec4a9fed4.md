- **Free space** — If your entire hard disk consists of a single Windows partition, you can resize your existing partition to use some of the free space to assign to Linux partitions. Note the amount of free space you have here and compare it to the amounts you will need to install Linux (described earlier).

Despite the fact that I have successfully resized several NTFS partitions using the **GParted** utility, I still recommend caution (and a good backup of your data) before proceeding. I have listed a few commercial products to resize your partitions here, in case you feel more comfortable using those. I have not tested the products so I name them here only because I have heard good reports of success from others:

- **Norton Partition Magic** — I’ve heard good reports from people using Partition Magic (http://www.symantec.com/norton/partitionmagic) to resize NTFS partitions. Partition Magic also helps you create new partitions and manage them. It supports Windows XP Professional/Home, Windows 95b-98SE, Windows Me, Windows 2000 Professional, and NT 4.0 workstation (SP6a). **Acronis OS Selector** — This is another well-regarded product for managing, creating, and resizing partitions, which is now included in the Acronis Disk Director Suite (http://www.acronis.com). It supports a variety of file system types, including FAT12, FAT16, FAT32, NTFS, and Linux partition types (ext2, ext3 and Linux ReiserFS). It also supports the same Windows platforms that Partition Magic does.

> **NOTE:** **Earlier releases** of Fedora included a FIPS utility for resizing FAT and VFAT file systems. FIPS is no longer included with Fedora, so no description of FIPS is included here.

Microsoft Windows Vista comes with tools for resizing your disk partitions. From the Start menu, right-click on Computer and select Manage. In the left pane that appears, select Storage and click Disk Management. Then right-click on the volume you want to resize and select either Extend Volume or Shrink Volume to change its size.

The open source tool I describe here for resizing your disk is called **GParted**. It can be used to resize partitions that contain a variety of file system types.

If your Windows system is backed up and your disk defragmented, you can begin the process of resizing your NTFS or VFAT disk partition with GParted using the Fedora 12 Desktop Live CD included with this book. Here’s how to resize your NTFS partitions using that CD:

+   1. Insert the Fedora 21 Desktop Live CD and reboot your computer.
+   2. At the boot prompt, with the first entry highlighted, press Enter .
+   3. When the Desktop Live CD boots to a GNOME desktop, to begin resizing your hard disk you need to install the gparted package. Assuming you have an Internet connection, type the following from a Terminal window:

```
```
$ su -
# yum install gparted
```
```