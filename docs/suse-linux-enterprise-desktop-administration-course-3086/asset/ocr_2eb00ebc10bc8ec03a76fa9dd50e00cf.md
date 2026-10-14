+   - *Reiser*—Formats the partition with ReiserFS, a modern journaling file system. (This is the default option.)
+   - *FAT*—Formats the partition with the FAT file system. FAT is an older file system used in DOS and Windows. You can use this option to create a data partition which is accessible from Windows and Linux. You must not create a root partition with this file system.
+   - *XFS*—Formats the partition with XFS, a journaling file system originally developed by SGI.
+   - *Swap*—Formats the partition as a swap partition.

If you are not sure which file system to choose, select Reiser for root and data partitions and Swap for swap partitions.

![](bbox=[0.113, 0.267, 0.299, 0.339])

+   - *Options*—Allows you to change parameters for the file system you selected. You can use the default parameters in most cases.
+   - *Encrypt file system*—Encrypts the partition with the file system. Encrypting a file system prevents unauthorized mounting only; once mounted the files are accessible like any other file on the system.
+     You should only use this option for nonsystem partitions such as user home directories.
+   - *Size*—Lets you configure the size of the new partition with the following:
+     - *Start Cylinder*—Determines the first cylinder of the new partition. YaST normally preselects the first available free cylinder of the hard disk.
+     - *End*—Determines the size of the new partition. YaST normally preselects the last available free cylinder. To configure the end cylinder, do one of the following:
+       - Enter the cylinder number.
+       - Enter a plus sign (+) followed by the amount of disk space for the new partition. Use M for MB and G for GB. YaST calculates the last cylinder number.
+       - For example, enter +5G for a partition size of 5 GB.
+   - *Fstab Options*—Allows you to edit the fstab entry for this partition. The default setting should work in most cases.
+   - *Mount Point*—Allows you to select the mount point of the new partition from this drop-down list. You can also enter a mount point manually, if it is not available in the list. The mount point will be created automatically during installation.