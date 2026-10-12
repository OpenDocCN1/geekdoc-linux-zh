Issues related to resizing NTFS file systems and finding tools to do so are contained on the Ntfsresize FAQ (mlf.linux.rulez.org/mlf/ezaz/ntfsresize.html). One bootable Linux described there that includes NTFS resizing tools is the System Rescue CD project. You can download, burn and boot the System Rescue CD to resize your NTFS partition. Here’s how:

+   1. Go to the System Rescue CD site and download the latest System Rescue CD (www.sysresccd.org/SystemRescueCD_en.php).

+   2. Burn the System Rescue CD image to a CD. (Chapter 5 describes how to burn CDs.)

+   3. Insert the System Rescue CD into the computer containing the NTFS file system you want to resize and reboot the computer (press Enter at the boot prompt).

+   4. When System Rescue CD finishes booting, type the following to resize your hard disk:
+   
+       # run_qtparted

+   5. When the run_qtparted window opens, select the hard disk (from the left column) that you want to resize. The partitions on that hard disk appear on the right column.

+   6. Select the Windows partition you want to resize (a Windows icon will appear next to the partition), then choose Operations→Resize.

+   7. In the box that appears, click the down arrow next to the amount of disk space on the partition to free some of its space for resizing.

+   8. Click File→Commit to commit the changes.

At this point, the free space you indicated when you resized your NTFS partition should be available to use to install Fedora Core. If you feel more comfortable resizing your hard disk using a commercial product, there are several such products available today:

> CAUTION: Despite the fact that I have successfully resized several NTFS partitions using the run_qtparted utility, I still recommend caution (and a good backup of your data) before proceeding. As for the commercial products listed below, I have not tested the products so I name them here only because I have heard good reports of success from others. User beware.

+   • **Partition Magic** — I’ve heard good reports from people using Partition Magic (www.powerquest.com/partitionmagic) to resize NTFS partitions. Partition Magic also helps you create new partitions and manage them. It supports Windows XP Professional/Home, Windows 95b-98SE, Windows Me, Windows 2000 Professional, and NT 4.0 workstation (SP6a). The cost is currently $69.95.

+   • **Acronis OS Selector** — This is another well-regarded product for managing, creating, and resizing partitions, which is not included in the Acronis Disk Director Suite. It supports a variety of file system types, including FAT12, FAT16, FAT32, NTFS, and Linux partition types (ext2, ext3 and Linux ReiserFS). It also supports the same