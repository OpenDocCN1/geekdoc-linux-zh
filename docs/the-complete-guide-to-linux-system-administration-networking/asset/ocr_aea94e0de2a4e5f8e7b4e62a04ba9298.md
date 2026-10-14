+   1. Start fdisk with the device name of the new hard disk:
+      fdisk /dev/hdb
+   2. Type p to list the partitions currently defined on the hard disk. (On a new hard disk there may be none.)
+   3. If you are using an old hard disk that contains existing partition data, enter d, followed by the partition number when prompted, to delete each partition on the hard disk. (Remember, you're only deleting the definition from a memory copy of the partition table; you can press Ctrl+c to exit fdisk if you become uncertain of what you're doing.)
+   4. Enter n to begin creating a new partition.
+   5. Enter p for primary partition. (You can create more than four partitions on a hard disk using extended, or logical, partitions, but you shouldn't need to do this.)
+   6. Enter a partition number for the partition you are creating. For this value, enter the next free partition on the hard disk. On a brand new hard disk, the number you enter should be 1.
+   7. Begin to define the size of the new partition by entering its first cylinder as requested. The range of available cylinders on the hard disk is listed in parentheses, like this:
+      First cylinder (1-1526, default 1):
+   8. Finish defining the size of the partition. To do this you can enter either a size, or a cylinder number. Example sizes you can enter are +900M for a 900 MB partition, or +4G for a 4 GB partition. To use the entire hard disk as a single partition, enter the last cylinder number displayed in the fdisk prompt.
+   9. Specify the partition type by entering t. The partition type informs any operating system that looks at the partition table in what format the data is stored on the partition.
+   10. Enter the type code for a Linux native partition, which is 83. (At this point you can enter l (lowercase letter "L"), for "list," to see a listing of partition type codes, which is interesting to review.)

> NOTE
> If you specify a cylinder number rather than a size to finish defining a partition, you can learn the actual size of the partition only by using the p command to list the partitions and the size of each.