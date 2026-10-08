# # Move Over, Windows — Here Comes Linux

You need to make room for Linux. This section describes how to repartition your Windows computer to make the necessary room. You can use the Open Source FIPS program to repartition FAT partitions. FIPS doesn't work on NTFS partitions, so you need to purchase a commercial tool, such as PartitionMagic. The next section is dedicated to using FIPS on FAT. The subsequent section describes using the commercial PartitionMagic program on NTFS partitions.

![](bbox=[0.12, 0.34, 0.2, 0.42])

We strongly suggest backing up your entire computer before proceeding. If that's impractical or impossible, you should back up all important files. You can generally reinstall your operating system and applications from your systems discs, but you can't do that for your data. You don't want to lose any data or programs that you worked hard to create. Refer to your system's owner's manual to find out how to back up your system and how to restore the data if necessary.

# ## Resizing Windows 9x and Windows Me FAT partitions with FIPS

FIPS resizes your FAT-based Windows partitions. Newer versions of Windows (some versions of Windows 95, Windows 98, and Windows Me) use a 32-bit file allocation table (called FAT32) and drive management tools that provide for single-drive configurations larger than 2GB. Older versions of Windows 95 use a 16-bit FAT (called FAT16, oddly enough); to use more space over and above 2GB, the hard drive has to be partitioned into logical drives of 2GB or less. Newer computers have hard drives much larger than the old 2GB limit. If the drive is repartitioned, the large drive-management system is disabled, and DOS and Windows partitions are again limited to 2GB.

You need to use the ancient MS-DOS (Microsoft Disk Operating System) operating system — yes, one way or another, all of Windows-dom owes its existence to MS-DOS. The following instructions describe how to create an MS-DOS boot floppy disk, which you use to run FIPS:

![](bbox=[0.12, 0.81, 0.2, 0.89])

+   1. **Insert a floppy disk and click the My Computer icon.**
   Please be aware that these instructions permanently erase all information from the disk.