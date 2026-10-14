+   - If you have three primary partitions and an extended partition, you can only create logical partitions.

![](bbox=[0.104, 0.134, 0.295, 0.207])

You need enough space on your hard disk to create a new partition. Later in this section you learn how to delete existing partitions to free used disk space.

If you choose to create either a primary or a logical partition, the screen shown in Figure 1-9 appears.

![](bbox=[0.109, 0.279, 0.721, 0.577])

**Figure 1-9**

This dialog provides the following options:

+   - *Format*—This lets you choose one of the following options:
+     - *Do not format*—Leaves the newly created partition unformatted. No file system will be created on this new partition. You can select the partition type in the drop-down list.
+     - *Format*—Formats the new partition with the file system you select from the File system drop-down list. You can choose from the following file systems:
+     - *Ext2*—Formats the partition with the Ext2 file system. Ext2 is an old and proven file system, but it does not include journaling.
+     - *Ext3*—Formats the partition with the Ext3 file system. Ext3 is the successor of Ext2 and offers a journaling feature.