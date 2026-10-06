# Part I: Getting Started in Fedora and RHEL

+   - **Partition Magic** — I've heard good reports from people using Partition Magic (http://www.symantec.com/norton/partitionmagic) to resize NTFS partitions. Partition Magic also helps you create new partitions and manage them. It supports Windows Professional/Home, Windows 95b-98SE, Windows Mc. Windows 2000 Professional, and NT 4.0 runtime (SP6a). The cost is currently $69.95.

+   - **Acronis OS Selector** — This is another well-regarded tool for managing, creating, and resizing partitions, which is now included in the Acronis Disk Director Suite. It supports a variety of file systems, including FAT12, FAT16, FAT32, NTFS, and Linux partition types (ext2, ext3 and Linux ReiserFS). It also supports the same Windows platforms that Partition Magic does. The cost is currently $49.99 from http://www.acronis.com.

> NOTE: Earlier releases of Fedora included a FIPS utility for resizing FAT and VFAT file systems. FIPS is no longer included with Fedora or RHEL, so no description of FIPS is included here. A description of FIPS from an earlier edition of this book is at the Wiley Web site: http://www.wiley.com/fedoraBible.

Microsoft Windows still comes with tools for resizing your partitions. From the Start menu, right-click on Computer and select Manage. In the left pane that appears, select Storage and click Disk Management. Right-click on the window you want to resize and select Extend Volume to change its size.

The open source tool I describe for resizing your disk is called GParted. It can be used to resize partitions that contain a variety of file system types.

If your Windows system is backed up and your disk defragmented, you can begin the process of resizing your NTFS or VFAT disk partition with GParted using the Fedora 10 Desktop Live CD included with this. Here's how to resize your NTFS partitions using CD:

+   1. Insert the Fedora 10 Live CD and reboot your computer.
2. At the boot prompt, with the first entry highlighted, press Enter.
3. When the live CD boots to a KDE desktop, begin resizing your hard you need to install the gparted package. Assuming you have an Internet connection, type the following from a Terminal:

```
$ su -
# yum install gparted
```

+   4. From the KDE menu, search for the GParted application and select it. The GParted graphical partitioning tool /dev/ displaying your current disk partitions.

+   5. Select the disk (probably /dev/sda) and partition (probably NTFS or VFAT for a Windows partition) you want to resize. The Resize/Move button should become available.