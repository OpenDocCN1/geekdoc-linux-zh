
## Default Solaris 8 File Systems

The disk space available for use with a Solaris 8 operating system is a collection of mounted file systems. The top directory is the location where the root file system is mounted. The locations where other file systems are mounted, called *mount points*, are subdirectories of the root file system, and normally are used to refer to the file systems themselves. For example, the file system mounted at /usr normally is referred to as the /usr file system. Table 9.2 lists the default file systems of a Solaris 8 operating system.

**Table 9.2  Default File Systems**

| File System | Use |
|---|---|
| root (/) | The top of the hierarchical file system tree. Contains critical system files, such as the kernel and device drivers. |
| /usr | System files, such as commands and programs, used to administer and use the system. |
| /home | User home directories. On some systems, it might be /export/home or a network-based file system. |
| /var | System files that change or grow, such as logs, queues, and spooling areas. |
| /opt | Third-party software and applications. |
| /tmp | Temporary files cleared each time the system boots. |
| /proc | Information on active processes. |

These file systems are UFS file systems. The two memory-based file systems (/tmp and /proc) are type TMPFS and PROCFS, respectively.

![](img/b957f979417d9f16274c2eb52c8f2c9f_221_0.png)

Because kernel files reside in the root file system and system files reside in the /usr file system, these two file systems are required to boot a usable system.

### Creating UFS File Systems

You can use the **mkfs(1M)**, **mkfs_ufs(1M)**, and **newfs(1M)** commands to create a UFS file system. The **mkfs_ufs** command is typically not used directly. It is called by the **mkfs** command when **mkfs** is used to create a UFS file system. The **newfs** command is the preferred method for creating a UFS file system because it provides a user-friendly interface to the **mkfs** command.

The **newfs** command calculates the appropriate parameters and calls the **mkfs** command to create the file system. You can specify command-line arguments to override the calculated parameters. The only required command-line argument is the raw logical device name of the partition in which the file system should be created. The following example uses the **newfs** command to create a UFS in a 1GB partition. The **-v** command-line argument specifies *verbose mode*, which causes the **newfs** command to display its actions:

```text
# newfs -v /dev/rdsk/c0d1s7
newfs: construct a new file system /dev/rdsk/c0d1s7: (y/n)? y
mkfs -F ufs /dev/rdsk/c0d1s7 2104515 63 240 8192 1024 ... 8 7
Warning: 12286 sectors (5) in last cylinder unallocated
/dev/rdsk/c0d1s7: 2104514 sectors in 140 cylinders of 240 tracks,
    63 sectors
 1027.6MB in 24 cyl groups (6 cg, 44.30MB/g, 10688 i/g)
super-block backups (for fsck -F ufs -o b=#) at:
  32, 90816, 181600, 272384, 363168, 454352, 545136, 635920,
  726304, 817088, 907872, 998656, 1089440, 1180224, 1271008,
  1361792, 1452576, 1543360, 1634144, 1724928, 1815712,
  1906496, 1997280, 2088064,
#
```

Another useful **newfs** command-line option is **-N**, which causes the **newfs** command to calculate the parameters that will be used to call the **mkfs** command; however, the **mkfs** command is not actually called, and the file system is not created. The **-v** command-line argument is used to preview the file system parameters. In addition, most of the **mkfs** command-line arguments can be specified as **newfs** command-line arguments. If any of them are specified, they override any calculated parameters and are passed to the **mkfs** command. See the **newfs(1M)** and **mkfs(1M)** manual pages for details.

If you’re using the **mkfs** command directly, you should include the **-F** command-line argument to identify the type of file system to create. If you don’t specify a file system type, the type listed in the /etc/default/fs file is used by default. The default type for local (disk-based) file systems is UFS. Additional parameters, such as block size and disk geometry (sectors per track, tracks per cylinder, and so on) can also be specified.

![](img/b957f979417d9f16274c2eb52c8f2c9f_222_0.png)

The commands used to create file systems expect raw (character) logical device names. In addition, the only type of disk-based file system that can be created on a standard Solaris 8 operating system is UFS. However, when a floppy disk is formatted, the PCFS is created on the floppy disk automatically.

### Checking and Repairing File Systems

File systems are damaged when the data defining them is corrupted. This corruption can be caused by software errors or by failures of the underlying physical disk hardware. The fsck(1M) command checks (audits) the logical consistency of a file system and attempts to make the repairs necessary to eliminate any inconsistency. The fsck command checks the superblock, inodes, indirect blocks, and directory data block.

The fsck command is typically executed when a file system is mounted automatically as part of system boot. It can also be executed manually on one or more file systems. Only unmounted file systems should be checked and repaired because changes can affect programs accessing the file system and in turn cause even more damage. One or more raw logical device names (partitions) can be specified as command-line arguments. As with the mkfs command, you should use the -F command-line argument to specify the type of file system being checked. The following example shows using the fsck command to check the 1GB file system previously created:

```text
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

![](img/b957f979417d9f16274c2eb52c8f2c9f_223_0.png)

Like the commands used to create file systems, the fsck command expects raw logical device names. You can use the fsck command to check and repair CacheFS, UDF, and UFS file systems. Remember to unmount the file system first.

### Mounting and Unmounting File Systems

File systems are made accessible by using the mount(1M) command. This command associates (mounts) the file system with a subdirectory of a currently mounted file system.

The mount command typically is called with two command-line arguments: a logical block device name (partition) associated with a file system, and a mount point where the file system should be mounted. If only one command-line argument is specified (device name or mount point), the /etc/vfstab file is searched for an entry matching the argument; if found, the file system is mounted using the information from the /etc/vfstab file entry. In addition, the **-F** command-line can identify the type of file system being mounted. Mounted file systems are listed in the /etc/mnttab file (unless the **-m** command-line argument is specified). If the **mount** command is used with no command-line arguments, all mounted file systems listed in the /etc/mnttab file are displayed.

The **mount** command supports several options specified as command-line arguments. One significant option is UFS large file support. By default, UFS file systems support large files (more than 2GB). This default is the same as specifying **-o largefiles** as a command-line argument. To disable large file support, specify **-o nolargefiles** as a command-line argument to the **mount** command. If this option is specified and a large file exists on the file system, the mount will fail.

Table 9.3 lists the commonly used command-line arguments for the **mount** command.

**Table 9.3 Selected mount Command-Line Arguments**

| Argument | Use |
|---|---|
| **-F type** | Specify the type of file system (NFS, UFS, and so on) |
| **-m** | Mount the file system without making an entry in /etc/mnttab |
| **-o** | Specify file-system-specific options |
| **-p** | List the mounted file systems (abbreviated listing) |
| **-r** | Mount the file system as read-only |
| **-v** | List the mounted file systems (verbose listing) |

Multiple file-system-specific options (**-o**) can be specified separated by commas. Following are some of the frequently used UFS options:

- **atime**—Use normal access time recording (default).
- **intr**—Allow keyboard interrupts to kill processes waiting on file system I/O (default).
- **largefiles**—Allow files larger than 2GB (default).
- **noatime**—Reduce file system activity by not updating file access times.
- **nointr**—Do not allow keyboard interrupts to kill processes waiting on file system I/O.
- **nolargefiles**—Do not allow files larger than 2GB. If any exist in the file system, the mount will fail.
