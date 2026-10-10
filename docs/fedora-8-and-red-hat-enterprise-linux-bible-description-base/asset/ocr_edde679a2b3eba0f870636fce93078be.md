# Chapter 2: Installing Fedora 63

> Red Hat, Inc. encourages you to use VFAT file systems for your Windows partitions if you plan to dual boot your computer with Linux. In Fedora 8, for the first time, Fedora offers support for the NTFS file system type. So you can now use tools from within Fedora to resize your Windows NTFS partitions.
> If, after resizing your Windows partitions and installing Fedora or RHEL, your computer becomes unbootable, refer to the “Troubleshooting Installation” section later in this chapter for advice on what to do.

Before you begin resizing your Windows system, boot Windows and do the following:

+   - **Back up your data!** Of course, you should always have a current backup of your important data. However, now is a particularly good time to do a back up, just in case one of those disk catastrophes I warned you about actually happens.
+   - **Defragment your disk.** Before you resize your hard disk, you should use a defragmenting utility in Windows to have all files stored contiguously on the disk. That way, when you reassign free space to Linux partitions, you have a continuous area of the disk to work with. To defragment a disk in Windows XP, click **Start \u2192 All Programs \u2192 Accessories \u2192 System Tools \u2192 Disk Defragmenter**. Then select **Defragment** from the Disk Defragmenter window. Defragmenting can take a while, depending on your processor speed and disk size.

While you have the Disk Defragmenter window displayed, note a few things about your hard disk that you will need to know later:

+   - **File System** — The file system type will most likely be NTFS, although it may also be VFAT. If you have the option to install Windows from scratch, selecting VFAT as the file system type will work much better for Linux. Support for writing to NTFS has been considered reliable from Linux, although reading from NTFS seems to work well. VFAT file systems, however, will work well for both Linux and Windows.
+   - **Free Space** — If your entire hard disk consists of a single Windows partition, you can resize your existing partition to use some of the free space to assign to Linux partitions. Note the amount of free space you have here and compare it to the amounts you will need to install Linux (described earlier).

Despite the fact that I have successfully resized several NTFS partitions using the GParted utility, I still recommend caution (and a good backup of your data) before proceeding. If you feel more comfortable using commercial products to resize your partitions, I have listed a few of those below. I have not tested the products so I name them here only because I have heard good reports of success from others:

+   - **Partition Magic** — I’ve heard good reports from people using Partition Magic (**www.powerquest.com/partitionmagic**) to resize NTFS partitions. Partition Magic also helps you create new partitions and manage them. It supports Windows XP Professional/Home, Windows 95b-98SE, Windows Me, Windows 2000 Professional, and NT 4.0 workstation (SP6a). The cost is currently $69.95.