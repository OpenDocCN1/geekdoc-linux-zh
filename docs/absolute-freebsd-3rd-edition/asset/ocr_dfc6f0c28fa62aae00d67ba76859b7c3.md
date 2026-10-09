its own disklabel, listing the BSD partitions contained within the slice. If you come from a Linux or Microsoft Windows background, the MBR partitions you're familiar with are called slices over here.

You can't label slices or disklabel partitions. These formats have no space for labels. Instead, label the ZFS or UFS filesystem on the partition.

It's possible to skip slicing a disk, instead installing a disklabel directly on the hard drive. Some hardware refused to boot from such disks, so they're called dangerously dedicated. With the advent of GPT, dangerously dedicated disks aren't really used any more.

# ## MBR Device Nodes

Every disk, slice, and partition has a device node. The slice device node is an extension of the underlying disk, and the partition device node is an extension of the device's node. Here are the device nodes on disk ada0 of an MBR-based system:

| | | |
|:---|:---|:---|
| /dev/ada0 | /dev/ada0s1a | /dev/ada0s1d |
| /dev/ada0s1 | /dev/ada0s1b | /dev/ada0s1e |

The first subdivision of the disk is the slice. Device nodes indicate a slice with the letter s and a number from 1 to 4. The first slice is s1, the second is s2, and so on. Unused MBR partitions don't get device nodes. Here, /dev/ada0s1 is slice 1 on the disk.

The second layer of subdivision is the disklabel partition inside the slice. Each partition has a unique device node name created by adding a letter to the slice's device node. Here, we have four disklabel partitions, /dev/ada0s1a through /dev/ada0s1e. Traditionally, the node ending in a (/dev/ada0s1a) is the root partition, while the node ending in b (/dev/ada0s1b) is swap space.

Note that the list of device nodes doesn't use the letter c. The c partition represents the entire slice. These days, you run disk partitioning tools on the slice entry rather than the disklabel for the slice.