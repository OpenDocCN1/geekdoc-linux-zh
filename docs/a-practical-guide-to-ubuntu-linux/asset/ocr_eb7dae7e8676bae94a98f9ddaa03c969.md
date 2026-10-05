The directory that you mount a filesystem is called a mount point. The directory you specify when you use the installer to create a partition is the mount point for the partition. Most mount points are top-level subdirectories, with a few exceptions (such as /usr/local, which is frequently used as a mount point).

# Do not create files on mount points before mounting a filesystem

Do put any files in a directory that is a mount point while a filesystem is not mounted on that mount point. Any files in a directory that is used as a mount point are covered up while the filesystem is mounted on that directory; you will not be able to access them. They reappear when the filesystem is unmounted.

For example, suppose the second partition on the first hard has the name /dev/sda2. To create an ext4 filesystem that you want to appear as /home in the /dev/sda2 hierarchy, you must instruct Linux to mount the /dev/sda2 partition as /home when the system boots. With this filesystem mounted on its normal point, you can access it as the /home directory.

The state of one filesystem does not affect other filesystems: One filesystem on a drive may be corrupt and undesirable, while other filesystems function normally. One filesystem may be full so you cannot write to it, while others have plenty of room for more data.

The file that holds the information relating to mount points is /etc/fstab (filesystem table; page 510). The associations stored in fstab are the normal ones for the system, but you can override them. When you work in recovery mode, you mount a filesystem on the /target directory so you can repair the filesystem. For example, if you mount on /target the partition holding the filesystem normally mounted on /home, the directory you normally find at /home/sam will be found at /target/sam.

A partition and any filesystem has no name or identification other than device name (and a UUID value—see page 510). Instead, the partition and the filesystem are frequently referred to by the name of the partition's normal mount point. Thus “the home partition” and “the home filesystem” refer to the partition that holds the filesystem normally mounted on the /home directory. See page 506 for information on mounting filesystems.

# PARTITIONING A DISK

During installation, the installer calls a partition editor to set up disk partitions. This section discusses how to plan partition sizes. Although this section uses the term partition, planning and sizing LVs (logical volumes; page 41) works the same way. For more information refer to pages 64 and 70 and to the Linux Partition HOWTO at www.tdp.org/HOWTO/Partition.

# GUIDED PARTITIONING

It can be difficult to plan partition sizes appropriately if you are not familiar with Linux. During installation, Ubuntu provides guided partitioning. Without asking