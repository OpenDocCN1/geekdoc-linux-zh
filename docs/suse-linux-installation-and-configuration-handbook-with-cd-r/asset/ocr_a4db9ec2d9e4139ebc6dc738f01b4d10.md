When Partition Resizer starts, it will scan for the available hard disks you have and check the partitions on each disk. It will then give you the following options:

+   - 1: Resize/Move a partition
+   - 2: Change a FAT16 partition's cluster size (Destructive)
+   - 3: Partition information
+   - 4: Exit

By pressing 1, you will get a list of all the available partitions on all your disks. The list has the following format:

+   - **(No.)**—The number you type to choose to resize or move this partition.
+   - **Flags**—The flags set to this partition. The list of flags is written at the same screen.
+   - **System Type**—The filesystem in which the partition was formatted. Partition Resizer can resize only FAT16 and FAT32 partitions.
+   - **Letter**—The drive letter of the corresponding partition.
+   - **Serial Number**—The serial number of the partition.
+   - **Size**—The current size of the partition.

If you type in the number of the partition you want to move or resize and press Enter, you will move to the Partition Resizer resize/move screen.

**TIP** To move to the previous screen in any screen of Partition Resizer, you can use the ESC button.

# Partition Resizer Controls

While in the resize/move mode, you can resize or move the partition you selected in the previous step. The following are controls you can have over this partition:

+   - **Tab key**—The tab key changes the mode from resize to move or vice versa. Partition Resizer starts in resize mode.
+   - **Arrow keys**—While in resize mode, the arrow keys are used to change the size of the partition. Alternatively, while in move mode, the arrow keys are used to move the partition. The left/right arrow keys will resize/move in small increments, whereas the up/down keys will resize/move in large increments.
+   - **Spacebar**—The spacebar is used to show/hide the extended partition boundaries. If you are resizing/moving a logical partition, you can't exceed the extended partition boundaries.

Use the previous controls to change the size of the selected partition. When you are finished, press Enter for the changes to take effect. If you want Partition Resizer to perform a surface