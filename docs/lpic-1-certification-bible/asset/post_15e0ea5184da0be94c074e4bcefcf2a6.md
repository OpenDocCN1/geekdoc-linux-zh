
The options used by `mkfs` are followed by an argument specifying the partition that is to be formatted. After the command has been run an exit code of 0 (zero) will indicate success while the exit code of 1 (one) indicates failure. An example of the syntax used is as follows:

```
mkfs -option argument
```

When creating a file system using `mkfs`, several commands can be used to specify the file system type. Table 5-5 shows the various commands to use when creating file systems. As you can see, there are specific commands to run for each file system type you want to create. These commands are accessible only by the root user.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_243_0.png)

> The utilities to understand for the test, and for real world usage, are covered here. Each file system type is created using a specific command. Be sure to know which commands are used for creating ext2, swap, and MS-DOS file systems.

### Table 5-5 Utilities for File System Creation

| Command | Use |
| :--- | :--- |
| `mkfs.ext2` or `mke2fs` | Creates an ext2 file system. |
| `mkfs.msdos` or `mkdosfs` | Creates an MS-DOS file system. |
| `mkswap` | Creates a Linux swap partition file system. |
| `mkraid` | Initializes and upgrades RAID device arrays. |
| `mkfs.minix` | Creates a Minix file system. |
| `mkfs.bfs` | Creates a SCO BFS file system. |

![](img/96d9ccd181675a8ae8b6a1146c919d2b_243_1.png)

More details on the options available when creating each file system can be located in the Linux man pages.

To create a file system the correct tool specified in Table 5-5 must be used. An example of the proper use of these utilities is creating an ext2 partition using `mkfs.ext2` as shown below:

```
# mke2fs /dev/hda3
```

## Checking the File System

- **Objective 2.4 Devices, Linux File Systems, Filesystem Hierarchy Standard**
- *Maintain the integrity of file systems. Verify the integrity of filesystems, monitor free space and inodes, fix simple filesystem problems. Includes commands `fsck`, `du`, `df`.*

You only need to create a file system occasionally; most people configure their partitions and create file systems only once. The ongoing process is maintaining the file system. Linux provides several useful tools for verifying, monitoring, and fixing file systems. In this section we examine the tools used for these purposes: `fsck`, `du`, and `df`.

### fsck

The `fsck` utility is a file system checker utility that is useful for examining file systems to locate and possibly repair problems that are found. When specifying multiple file systems, the checks are run in parallel, unless you use the `-s` option to specify that they should be processed serialized. The `fsck` utility is similar to `mkfs` in that a different utility is used for each file system. Table 5-6 covers the `fsck` utilities and their use.

### Table 5-6 fsck Utilities

| Utility | Use |
| :--- | :--- |
| `e2fsck` or `fsck.ext2` | Linux ext2 file system checker |
| `dosfsck` or `fsck.msdos` | MS-DOS file system checker |
| `fsck.minix` | Minix file system checker |

When running these utilities you can use several options to control the actions taken. Table 5-7 shows the options used with the `fsck` utilities.

### Table 5-7 Options Used with fsck

| Option | Use |
| :--- | :--- |
| `-p` | Automatically repairs without prompting. |
| `-n` | Makes no changes to the file system. |
| `-y` | Assumes yes to all questions. |
| `-c` | Checks for bad blocks. |
| `-f` | Forces a check even if the file system is marked clean. |
| `-r` | Interactively prompts for changes. |
| `-v` | Be verbose. |
| `-b superblock` | Uses an alternative superblock. |
| `-1 badblocks-file` | Adds to bad blocks list. |
| `-L badblocks-file` | Sets bad blocks list. |
| `-A` | Checks all file systems listed in `/etc/fstab`. |
| `-C` | Displays a completion/progress bar. Currently only works for ext2 file systems. |
| `-N` | Doesn't execute, simply displays what would be done. |
| `-P` | Used with -A; processes the root file system in parallel with others. |
| `-R` | Used with -A; causes the root file system to be skipped. |
| `-V` | Displays version information. |

These options are especially useful for specifying bad blocks and the superblock. The ability to specify an alternative superblock allows for the file system to be recovered in the case of a corrupt or damaged superblock. Copies of the superblock are stored throughout the disk, and an alternative superblock can be specified. As mentioned earlier in this chapter, a backup superblock is stored at throughout the file system.

During the `fsck` check of a system the following is done:

- Pass 1: Checking inodes, blocks, and sizes
- Pass 2: Checking directory structure
- Pass 3: Checking directory connectivity
- Pass 4: Checking reference counts
- Pass 5: Checking group summary information

Normally during system boot, `fsck -p` is run to check all file systems listed in the `/etc/fstab` file. This will automatically detect and fix problems with inodes, link counts, data blocks, and the superblock. If a more serious error is located, `fsck -p` will ask for help and then exit. Some of the errors that will cause this are as follows:

- Blocks claimed by multiple files
- Blocks claimed outside of the file system
- Too few link counts
- Unaccounted blocks
- Directories that correspond to unallocated inodes
- Format errors

In cases where the parent directory of a file cannot be determined, the file will be placed in `/lost+found`. Files here are renamed with their inode numbers. Examining the contents of this directory can be useful when missing files after a system error.

The exit information presented by the `fsck` utility provides useful information about the results of the operation. Each code represents a specific exit condition for the utility. The actual code returned is the sum of the exit conditions. The exit codes are displayed on the command line when the command has finished its operation. The exit codes are shown in Table 5-8.

### Table 5-8 fsck Exit Codes

| Code | Meaning |
| :--- | :--- |
| 0 | No errors. |
| 1 | File system errors corrected. |
| 2 | System should be rebooted. |
| 4 | File system error left uncorrected. |
| 8 | Operational error |
| 16 | Usage or syntax errors. |
| 128 | Shared library error. |

The `fsck` utility should not be run on currently mounted devices. When checking a device it is recommended that you first unmount the device and then run `fsck`. The following examples show the correct use of the `fsck` utility. First, the drive is unmounted so that `fsck` can access the partition. The first example performs a verbose check of the first partition on the second IDE drive. The drive is marked clean, and the number of used files versus possible files and used blocks versus total blocks is shown.

```
# mount /fun
# fsck.ext2 -v /dev/hdb1
e2fsck 1.18, 11-Nov-1999 for EXT2 FS 0.5b, 95/08/09
/dev/hdb1: clean, 9692/1237888 files, 1754206/2474002 blocks
```

In the second example a check is forcibly forced on the same partition. The drive is carefully examined and more detailed information regarding files, links, and blocks is displayed.

```
# fsck.ext2 -v -f /dev/hdb1
e2fsck 1.18, 11-Nov-1999 for EXT2 FS 0.5b, 95/08/09
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information

9692 inodes used (0%)
157 non-contiguous inodes (1.6%)
# of inodes with ind/dind/tind blocks: 1194/205/0
1754206 blocks used (70%)
0 bad blocks

8884 regular files
776 directories
0 character device files
0 block device files
1 fifo
0 links
22 symbolic links (22 fast symbolic links)
0 sockets

9683 files

# mount /fun
```

When you’re finished checking the drive, you must mount it for it to be available for use by the system.

### du

The `du` utility is used to report the amount of disk space used by the files and subdirectory for the specified directory. If no directory is specified for the utility, `du` works with the `pwd`, or present working directory. The user must have read access to the files and directories in order for this utility to run. The function of the `du` utility can be controlled using a variety of options, which are covered in Table 5-9.
