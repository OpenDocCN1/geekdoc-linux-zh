# Other Partitions

The next dialog presents a list of most of the disk partitions on your system (including MS-DOS and other partitions Linux can read), giving you the opportunity to assign other partitions to different parts of the filesystem. The partitions you assign will be automatically mounted when your Red Hat Linux system boots. Select the partition you wish to assign and press **Enter** (or choose *Edit*; then enter the *mount point* for that partition, e.g., `/usr` (see Figure 2.12)).

![](bbox=[0.26, 0.34, 0.88, 0.61])

Figure 2.12: Filesystem Configuration

Additionally, Red Hat Linux allows you to mount NFS volumes when your system boots; this allows directory trees to be shared across a network. Choose **Add NFS**; then enter the hostname of the NFS server, the path to the NFS volume, and the local mount point for that volume (see Figure 2.13).

# Formatting Partitions

The next installation dialog presents a list of partitions to format. Most partitions should be formatted, especially if they are newly created; however, partitions such as `/home` or `/usr/local` do not need to be formatted if they contain data you wish to keep. Select each partition to format and press **Space**. If you wish to check for bad blocks while formatting each