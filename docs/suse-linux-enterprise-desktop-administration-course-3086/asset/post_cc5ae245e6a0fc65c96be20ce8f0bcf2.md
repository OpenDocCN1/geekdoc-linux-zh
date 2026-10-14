
- *Reiser*—Formats the partition with ReiserFS, a modern journaling file system. (This is the default option.)
- *FAT*—Formats the partition with the FAT file system. FAT is an older file system used in DOS and Windows. You can use this option to create a data partition which is accessible from Windows and Linux. You must not create a root partition with this file system.
- *XFS*—Formats the partition with XFS, a journaling file system originally developed by SGI.
- *Swap*—Formats the partition as a swap partition.

If you are not sure which file system to choose, select Reiser for root and data partitions and Swap for swap partitions.

![](img/9129877170834ca9d5fdac5319bf5f12_41_0.png)

- *Options*—Allows you to change parameters for the file system you selected. You can use the default parameters in most cases.
- *Encrypt file system*—Encrypts the partition with the file system. Encrypting a file system prevents unauthorized mounting only; once mounted the files are accessible like any other file on the system.
  You should only use this option for nonsystem partitions such as user home directories.
- *Size*—Lets you configure the size of the new partition with the following:
  - *Start Cylinder*—Determines the first cylinder of the new partition. YaST normally preselects the first available free cylinder of the hard disk.
  - *End*—Determines the size of the new partition. YaST normally preselects the last available free cylinder. To configure the end cylinder, do one of the following:
    - Enter the cylinder number.
    - Enter a plus sign (+) followed by the amount of disk space for the new partition. Use M for MB and G for GB. YaST calculates the last cylinder number.
    - For example, enter +5G for a partition size of 5 GB.
- *Fstab Options*—Allows you to edit the fstab entry for this partition. The default setting should work in most cases.
- *Mount Point*—Allows you to select the mount point of the new partition from this drop-down list. You can also enter a mount point manually, if it is not available in the list. The mount point will be created automatically during installation.

After changing the parameters, select **OK** to add the new partition to the partition list. If you chose to create an extended partition, the screen shown in Figure 1-10 appears.

![](img/9129877170834ca9d5fdac5319bf5f12_42_0.png)

**Figure 1-10**

You can enter the following:

- *Start cylinder*—The start cylinder determines the first cylinder of the new partition. YaST normally preselects the first available free cylinder of the hard disk.
- *End*—The end cylinder determines the size of the new partition. YaST normally preselects the last available cylinder of the hard disk. To configure the end cylinder, do one of the following:
  - Enter the cylinder number.
  - Enter a plus sign (+) followed by the amount of disk space for the new partition. Use M for MB and G for GB. YaST calculates the last cylinder number. For example, enter +5G for a partition size of 5 GB.

After entering the size, select **OK** to add the new extended partition to the partition list.

### Edit Existing Partitions
Select a partition from the list and select **Edit**. You can edit only primary and logical partitions with the Expert Partitioner. You cannot edit an extended partition or the entry for the entire hard disk.

If you edit a primary or logical partition, a dialog appears. It allows you to change all options except the partition size.

After changing the partition parameters, select **OK** to save your changes to the partition list.

### Delete Existing Partitions
To delete a partition, select a partition from the list, select **Delete**, and then select **Yes** in the confirmation dialog. The partition is deleted from the partition list.

Remember that you also delete all logical partitions when you delete an extended partition. If you select the entry for the entire hard disk and select **Delete**, all partitions on the disk are deleted.

## Resize Existing Partitions

![](img/9129877170834ca9d5fdac5319bf5f12_43_0.png)

Although you can reduce a partition’s size without deleting it to increase free space on the hard disk, you should always back up the data on the partition before resizing it.

![](img/9129877170834ca9d5fdac5319bf5f12_43_1.png)

If the selected partitions are formatted with the FAT or NTFS file system, there are certain steps you should take in Windows before resizing (scandisk and defrag). See the section on installation in the *SUSE Linux Enterprise Desktop 10 Deployment Guide* (`/usr/share/doc/manual/sled-deployment_en/manual/book.sled.deployment.html`, package sled-deployment_en) for details.

After you select **Resize**, the screen shown in Figure 1-11 appears.

![](img/9129877170834ca9d5fdac5319bf5f12_43_2.png)

**Figure 1-11**

This dialog includes the following:

- Two bars representing the partition before and after the resizing process
  - *Now*—Used space is designated by dark blue and the available space by light blue. Space that is not assigned to a partition is designated by white.
  - *After Installation*—Used space is designated by dark blue and the free space by light blue. Space that is available for a new partition is designated by white.
- A slider to change the size of the partition.
- Two text fields that display the amount of free space on the partition being resized and the space available for a new partition after the resizing process.
- A Do Not Resize button used to reset the partition to the original size.

To resize the partition, move the slider until enough unused disk space is available for a new partition. When you select OK, the partition size changes in the partition list.

### Perform Expert Tasks
When you select Expert, the following options are available:

- *Reread the Partition Table*—Resets the partition list to the current physical disk setup. All changes will be lost.
- *Import Mount Points from Existing /etc/fstab*—Scans the hard disks for an /etc/fstab file. You can load this file and set the mount points accordingly.
- *Delete Partition Table and Disk Label*—Deletes the partition table and the disk label of the selected hard disk. *All data on that disk will be lost.*

When you finish configuring settings in the Expert Partitioner, return to the installation proposal by selecting Finish.

The same YaST tool is available on the installed system to configure partitions. To perform similar tasks on the command line, you would use the fdisk command to add or delete partitions and mkfs to create file systems within these partitions. The manual pages for fdisk and mkfs explain the details. If you use fdisk or mkfs, you must, as the last step, edit the file /etc/fstab to make sure the file systems are mounted when the system starts.

## Select Software

SLED 10 contains many software packages for various application purposes. Instead of selecting needed packages one by one, you can select various software categories.

Depending on the available disk space, YaST preselects several of these categories. Selecting Software in the installation overview opens the dialog shown in Figure 1-12.

Figure 1-12 shows the default selection. A brief description appears on the right when you highlight a category in the center column.

To find out which packages are contained in the various categories, select Details, which opens the dialog shown in Figure 1-13.

Selecting one pattern on the left shows the software packages contained in that category on the right. Selecting the square to the left of the pattern selects it for installation or deselects it.

A package typically contains an application and all additional files required to use the software.

Sometimes larger applications can be split into multiple packages and several small applications can be bundled into a single package.

SUSE Linux Enterprise Software uses the RPM Package Manager for software management.

![](img/9129877170834ca9d5fdac5319bf5f12_44_0.png)
