On the rare occasions when a second run is needed, it should not turn up any more errors. If it does, you are most likely facing a hardware failure. Remember to start with the obvious: Check for reliable power and well-connected cables. Anyone running SCSI systems should verify that he’s using the correct type of terminator, that cables aren’t too long, that SCSI IDs aren’t conflicting, and that cable quality is adequate. (SCSI is especially fussy about the quality of the cables.)

# The /lost+found Directory

Another rare situation is when e2fsck finds segments of files that it cannot rejoin with the original file. In those cases, it will place the fragment in the partition’s lost+found directory. This directory is located where the partition is mounted, so if /dev/hda3 is mounted on /usr, then usr/lost+found correlates to /dev/hda3.

Anything can go into a lost+found directory—file fragments, directories, and even special files. When normal files wind up there, a file owner should be attached, and you can contact the owner and see if they need the data (typically, they won’t). If you encounter a directory in lost+found, you’ll most likely want to try and restore it from the most recent backup rather than trying to reconstruct it from lost+found.

At the very least, lost+found tells you if anything became dislocated. Again, such errors are extraordinarily rare.

# PARTITIONING A DISK

For the sake of clarity, and in case you need to know what a partition is and how it works, let’s do a brief review of this subject. Every disk must be partitioned. Partitions divide up the disk, and each segment acts as a complete disk by itself. Once a partition is filled, it cannot (without special software) automatically overflow onto another partition.

Usually, the process of partitioning a disk accomplishes one of two goals. Either the user needs two different operating systems installed and each operating system requires its own partition, or it may be prudent that the usage of space on one partition not interfere with space dedicated to other tasks on other partitions.

An example of the latter occurs in user home directories. When users of the system are not the administrators of the system, the administrator must ensure that users don’t consume the entire disk for their personal files. This takes up room needed for logging purposes and temporary files, causing the system to misbehave. To prevent this, a special partition is created for user files, so that they don’t overflow into protected system space.

> **NOTE:** It is acceptable to partition a disk so that only one large partition is taking up the entire disk.

# Where Disks Exist

Under Linux, each disk is given its own device name. IDE disks start with the name /dev/hdX, where X can range from a through z, with each letter representing a physical