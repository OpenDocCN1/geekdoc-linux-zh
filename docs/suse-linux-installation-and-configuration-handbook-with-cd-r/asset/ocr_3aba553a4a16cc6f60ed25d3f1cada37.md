# Using FIPS to Split Your Partitions

A very important utility that comes with SuSE Linux and runs under DOS is FIPS. FIPS can split a partition in two. You will appreciate this important feature if you have a big partition and you want to use a part of it to install SuSE Linux. SuSE Linux needs a partition for itself, so you must split your big partition and use one of the new ones to install SuSE Linux.

# What FIPS Does

To get the best results from FIPS, you need to understand how it works. FIPS will check how much space is left at the end of a partition. This space is the maximum you can tell it to use as a new partition. If you have files that reside at the end of a partition, you will not be able to split the partition, even though the partition has enough disk space. Figure 1.2 explains such a dilemma.

FIGURE 1.2
If you try to use FIPS to split the D: drive, you will be able to get only 500MB at maximum. You will not be able to split the E: drive, even though it has 1GB of free space. This is because the data lies at the end of the partition.

![](bbox=[0.3, 0.5, 0.92, 0.7])

# Preparing for FIPS

Before you use FIPS, you will need to do some preparation. If you were to prepare the D: and E: drives shown in Figure 1.2, you would perform the following steps:

+   1. Choose which partition you would like to split.
+   2. Consider the amount of space you will cut off this partition.
+   3. Run a disk check utility on this partition. Microsoft Windows comes with a ScanDisk utility that will do the job. Click Start, Accessories, System Tools, ScanDisk to start the ScanDisk utility.
+   4. Run a disk optimization utility on this partition. The disk optimization utilities have the advantage of moving all the used disk space to the beginning of the partition. Microsoft Windows comes with Disk Defragmenter. Click Start, Accessories, System Tools, Disk Defragmenter to start the Disk Defragmenter utility. Click the Setting button and check the Rearrange Program File So My Programs Start Faster check box.

Now the partitions should look like Figure 1.3.