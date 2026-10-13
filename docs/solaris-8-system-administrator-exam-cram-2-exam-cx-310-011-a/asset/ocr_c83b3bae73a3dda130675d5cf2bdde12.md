physical disk hardware. The fsck(1M) command checks (audits) the logical consistency of a file system and attempts to make the repairs necessary to eliminate any inconsistency. The fsck command checks the superblock, inodes, indirect blocks, and directory data block.

The fsck command is typically executed when a file system is mounted automatically as part of system boot. It can also be executed manually on one or more file systems. Only unmounted file systems should be checked and repaired because changes can affect programs accessing the file system and in turn cause even more damage. One or more raw logical device names (partitions) can be specified as command-line arguments. As with the mkfs command, you should use the -F command-line argument to specify the type of file system being checked. The following example shows using the fsck command to check the 1GB file system previously created:

```
    # fsck -F ufs /dev/rdsk/c0d1s7
    ** /dev/rdsk/c0d1s7
    ** Last Mounted on
    ** Phase 1 - Check Blocks and Sizes
    ** Phase 2 - Check Pathnames
    ** Phase 3 - Check Connectivity
    ** Phase 4 - Check Reference Counts
    ** Phase 5 - Check Cyl groups
    2 files, 9 used, 1019783 free
    #
```

If you don’t specify the -F command-line argument, the type of file system defined in the /etc/default/fs file (UFS) is used by default. In addition, if no partitions (raw logical device names) are specified, all the file systems listed in the /etc/vfstab file are checked.

![](bbox=[0.148, 0.634, 0.26, 0.701])

Like the commands used to create file systems, the fsck command expects raw logical device names. You can use the fsck command to check and repair CacheFS, UDF, and UFS file systems. Remember to unmount the file system first.

# Mounting and Unmounting File Systems

File systems are made accessible by using the mount(1M) command. This command associates (mounts) the file system with a subdirectory of a currently mounted file system.

The mount command typically is called with two command-line arguments: a logical block device name (partition) associated with a file system, and a mount point where the file system should be mounted. If only one command-line argument is specified (device name or mount point), the /etc/vfstab file is searched for an entry matching the argument; if found, the