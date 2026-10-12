Exactly what you do in Disk Druid depends on the hard drives in your PC and the partitions they already have. For this discussion, I assume that you have created the necessary hard disk space for Linux using one of the following methods:

+   - You start with a single hard drive with a single partition (only the C: drive in Windows). Then you use FIPS to split that partition into two. (Refer to the “Repartitioning Your Hard Drive with FIPS” section.) After partitioning, you end up with two DOS partitions.
+   - Your PC has a single, large hard drive (greater than 2GB) that has two partitions (C: and D: drives in Windows). In this case, the second partition has an extended partition that contains the logical drive D:. You want to install Red Hat Linux on the extended partition that used to be the D: drive in Windows.

Both of these situations call for the same sequence of steps, as outlined in the next two sections.

# Setting Up the Partitions

To prepare an existing DOS partition for Linux, you have to perform the following steps in Disk Druid:

+   1. Delete the DOS partition that you want to use for Linux. To do this, select the partition (typically the one with Device name hda2) from the Partitions list on the Disk Druid screen and then click the Delete button. Before deleting the partition, remember to make a note of the partition’s size from the Partitions list.
+   2. Create a new partition for the Linux file system. To do this, press the Add button on the Disk Druid screen. You should see a dialog box (refer to Figure 2-5) where you can fill in / as the mount point and enter the size in megabytes. To compute the size, simply subtract the size of the swap space (32MB or the amount of RAM in your PC, whichever is more) from the original size of the partition. Select the OK button and then press Enter to complete this step and return to the Disk Druid screen.
+   3. Create another new partition and set it as a Linux swap space. To do this, click the Add button in the Disk Druid screen (see Figure 2-4). In the dialog box (see Figure 2-5), enter the size of the partition. Click the list of partition types and use the mouse to select Linux Swap as the type. When you do so, the text <Swap Partition> appears in the Mount Point field. Next, click the OK button to define the new partition and return to the Disk Druid screen.