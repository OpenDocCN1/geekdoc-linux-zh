After you have installed Fedora, there are a few other useful things you might want to do so you can use files from your Windows partitions in Linux.

# **Using Windows partitions from Linux**

With some space available on your disk, when you go to install Linux, consider adding a small FAT16 or FAT32 partition (maybe 2GB) on your disk. Every x86 operating system (Linux, Windows 95, NT, 2000, XP, Vista, and DOS) supports those types. With that added, you will be able to freely exchange files between your Linux and Windows system on the FAT16 partition.

With FAT partitions, however, keep in mind that there are limitations. FAT is limited to between 2GB and 4GB file sizes. Also, FAT16 doesn’t support long filenames. Total partition size for FAT file systems is 32GB.

After you have installed Linux in the space freed up by the previous procedure, you should be able to choose between Linux and Windows when the Fedora boot screen appears during boot time. Press any key to go to the GRUB boot screen. Then move the arrow key to choose to boot Linux or Windows.

The first time you boot Windows, you might be asked to check your disk (because your Windows partition will be a different size than expected). After that, there should be no change in how you use your Windows system. Your disk space will just be smaller.

Now, when you boot up Linux, if you have a lot of documents, digital images, music, or other content on your Windows partition, you probably want to be able to use that content from Linux. To do that, you need to:

+   • Determine which partition is your Windows partition.
+   • Mount the Windows partition on your Linux file system.

The following procedure describes how to do those things.

1.  **Check partitions**. To determine which partition contains your Windows file system, use the `fdisk` command as follows:

```
# fdisk -l
Disk /dev/sda: 60.0 GB, 60011642880 bytes
16 heads, 63 sectors/track, 51280 cylinders
Units = cylinders of 1008 * 512 = 516096 bytes

Device Boot      Start         End      Blocks   Id  System
/dev/sda1 *          1         41725    21029053+  7  HPFS/NTFS
/dev/sda2         106741      116280    4808160  12  Compaq diagnostics
/dev/sda3          41725       41932     104422+  83  Linux
/dev/sda4          41932      106734    32660145  5  Extended
/dev/sda5          41932      106718    32652081  8e  Linux LVM
```