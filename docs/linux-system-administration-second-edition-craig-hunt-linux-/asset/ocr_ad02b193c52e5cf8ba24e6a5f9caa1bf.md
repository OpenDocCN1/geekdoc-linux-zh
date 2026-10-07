![](bbox=[0.11, 0.04, 0.89, 0.79])

Figure 3.1: A hard drive’s partition layout

Three of these (/dev/hda1 through /dev/hda3) are primary partitions that are pointed to directly, and two (/dev/hda5 and /dev/hda6) are logical partitions that reside within an extended partition (/dev/hda4). This baroque arrangement is the result of early limitations on the number of partitions in the PC’s partition table and is further discussed in Chapter 6, "Filesystems and Disk Management." Linux uses the Third Extended Filesystem (ext3fs), which is also detailed in Chapter 6. Basically, the filesystem is the structure imposed on each partition for the purpose of organizing