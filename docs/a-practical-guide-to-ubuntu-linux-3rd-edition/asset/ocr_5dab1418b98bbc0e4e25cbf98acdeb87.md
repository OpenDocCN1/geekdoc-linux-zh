![](bbox=[0.29, 0.08, 0.85, 0.35])

200-gigabyte (page 1150) hard disk on the device named /dev/sda. Figure 3-7 on page 61 shows the ubiquity partition editor ready to partition an empty drive similar to the one shown in Figure 3-11.

# RESIZING A PARTITION

Although you can resize a partition using the ubiquity partition editor while you are installing Ubuntu, you may find it easier to see what you are doing when you use the gparted partition editor from a live session for this task. This section explains how to use gparted to resize a partition.

# Always back up the data on a hard disk

> If you are installing Ubuntu on a disk that holds important data, back up the data before you start the installation. Things can and do go wrong. The power may go out in the middle of an installation, corrupting the data on the hard disk. There may be a bug in the partitioning software that destroys a filesystem. Although it is unlikely, you might make a mistake and format a partition holding data you want to keep.

Figure 3-12 (next page) shows gparted displaying information about a hard disk with a single partition that occupies the entire disk. This partition holds a single 200-gigabyte NTFS filesystem. The process of resizing a partition is the same regardless of the type of partition, so you can use the following technique to resize Windows, Linux, or other types of partitions.

To install Ubuntu on this system, you must resize (shrink) the partition to make room for Ubuntu. To resize the partition, right-click to highlight the line that describes the partition and click the arrow pointing to a line on the toolbar at the top of the window. The partition editor opens a small Resize/Move window, as shown in Figure 3-12.

At the top of the Resize/Move window is a graphical representation of the partition. Initially the partition occupies the whole disk. The spin box labeled New Size (MiB)