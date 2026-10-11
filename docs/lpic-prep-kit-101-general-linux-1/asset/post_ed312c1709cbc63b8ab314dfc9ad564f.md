
## Step 2: Create a Swap Partition

Next, you need to create a swap partition. When creating successive partitions, they should start with the next cylinder after the last one ended. Because our primary partition ended at 459, we will start the next one at 460:

```
Command (m for help): n
Command action
   e   extended
   p   primary partition (1-4)
p
Partition number (1-4): 3
First cylinder (460-788): 460
Last cylinder or +size or +sizeM or +sizeK (474-683): +128M
```

Display your partition scheme again using the `p` command and write down this information, especially the size of each partition in blocks.

```
Command (m for help): p

Disk /dev/hda: 255 heads, 63 sectors, 788 cylinders
Units = cylinders of 16065 * 512 bytes
```

| Device | Boot | Begin | Start | End | Blocks | Id | System |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/hda1 | * | 1 | 1 | 459 | 3686759 | 83 | Linux native |
| /dev/hda2 | | 460 | 460 | 475 | 128488 | 83 | Linux native |

In our example, the swap partition, /dev/hda2, is listed as a `Linux native` partition. To complete the creation of a swap partition, you must change the type to `swap` by using the `t` command:

```
Command (m for help): t
Partition number (1-4): 2
Hex code (type L to list codes): 82
```

```
Command (m for help): p
```

```
Disk /dev/hda: 255 heads, 63 sectors, 788 cylinders
Units = cylinders of 16065 * 512 bytes
```

| Device | Boot | Begin | Start | End | Blocks | Id | System |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/hda1 | * | 1 | 1 | 459 | 3686759 | 83 | Linux native |
| /dev/hda2 | | 460 | 460 | 475 | 128488 | 82 | Linux swap |

If you typed `L` instead of `82`, you will see that `Linux swap` is type `82` and `Linux native` is `83`. The type for extended partitions is `5`.

Be sure to review your partition table after each change to ensure that the changes you made are what you intended.

It is customary to create your primary and swap partitions before creating an extended partition. However, you can create a primary partition after creating an extended partition as long as there is free space available and you have not reached the four-partition limit.

## Step 3: Create an Extended Partition

Next, you should create an extended partition. Use the following:

```
Command (m for help): n
Command action
  e extended
  p primary partition (1-4)
e
First cylinder (476-788): 476
Last cylinder or +size or +sizeM or +sizeK (476-788): 788
```

When your partition table is displayed again, you'll see the following:

```
Command (m for help): p
Disk /dev/hda: 255 heads, 63 sectors, 788 cylinders
Units = cylinders of 16065 * 512 bytes
```

| Device | Boot | Begin | Start | End | Blocks | Id | System |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/hda1 | * | 1 | 1 | 459 | 3686759 | 83 | Linux native |
| /dev/hda2 | | 460 | 460 | 475 | 128488 | 82 | Linux swap |
| /dev/hda3 | | 476 | 476 | 788 | 2513751 | 5 | Extended |

Next, you will need to create logical drives in your extended partition. When you issue the `n` command, you will have a new choice:

```
Command (m for help): n
Command action
  l logical (4 or over)
  p primary partition (1-4)
```

You can elect to divide your extended partition into one or more logical drives by using the `l` command and then specifying the appropriate size. The starting and ending cylinders for each logical drive must be completely contained within the starting and ending cylinders of the extended partition.

After you have finished defining your partitions, you can quit `fdisk` and save the changes to the partition table by using the `w` command. If you decide you don't want to make these changes, use the `q` command to quit `fdisk` without saving your changes.

## Step 4: Assign Filesystem Names

Next, you must associate the appropriate Linux filesystem names with each of the partitions you are going to use. This is done through the installation program for your specific distribution. Remember, you can install Linux with only the `/` and `swap` partitions.

# The Linux Filesystem

The Linux filesystem organizes files and directories into a hierarchical structure. A filesystem provides a way to store files that can be randomly accessed, including hard disk partitions, floppy disks, and CD-ROMS. Because tape drives are accessed sequentially, they do not contain a true filesystem. Some of the common filesystems, not all of which are Linux filesystems, are:

- Extended Filesystem—ext (Linux, has been replaced by ext2)
- Fast Filesystem—ifs (Amiga)
- HPFS Filesystem—hpfs (used with the OS/2 operating system; supported in real-mode only)
- ISO9660 Filesystem—iso9660 (CD-ROM)
- Linux Swap Filesystem—swap
- Minix Filesystem—minix (Minix; this was the first filesystem used for Linux)
- MS-DOS Filesystem—FAT16 msdos (DOS)
- Network File System—nfs (Data is stored on any machine on a network and access is granted via the network)
- Novell Filesystem—NCPFS (Novell servers)
- NT Filesystem—NTFS (Windows NT)
- proc Filesystem—proc (Virtual filesystem used by the Linux kernel to provide information to the user about processes)
- Second Extended Filesystem—ext2 (Linux standard filesystem)
- System V Filesystem—sysv (System V variants; commercial UNIX systems for PCs)
- Uniform Filesystem—ufs (Used by BSD, SunOS, and NeXTstep; is supported in read-only mode)
- UMSDOS Filesystem—umsdos (UNIX on MS-DOS; applied on top of a FAT16 filesystem to provide Linux functionality by creating special files; is slow)
- Virtual FAT Filesystem—VFAT (an extension of the FAT filesystem to support long filenames)
- Xenix Filesystem—xenix
- Xías Filesystem—xiás (An old filesystem; hardly used anymore)

Within the Linux filesystem, the partition or hard drive you are accessing is invisible. Instead, each partition or hard drive is shown relative to the root of the filesystem. The root is represented as `/`.

If you have the following partitions:

```
hda1        /
hda2        swap
hda3        /var
hda4        /home
```

and issue an `ls /` command, the directory listing will appear and the `/var` and `/home` filesystems will show up as subdirectories residing with the `/` directory, even though they are located on different partitions.

# Formatting

Now that you have created your partitions, you must create a filesystem on each one before you can install Linux. Creating a filesystem on your hard disk is similar to formatting a floppy. You create a filesystem by using the `mkfs` command. Its syntax is:

```
mkfs -t fs-type device blocks
```

`mkfs` actually calls another command based on the type of filesystem you specify with the `-t fs-type` option. The various `mkfs` commands associated with specific filesystem types are shown in Table 3.3.

**Table 3.3** Commands Associated with Specific Filesystem Types Called by the `mkfs` Utility

| Command | Filesystem Type |
| :--- | :--- |
| `mkfs.ext2` | Create an ext2 filesystem; same as `mke2fs` |
| `mkfs.msdos` | Create an MS-DOS filesystem |
| `mkfs.minix` | Create a Minix filesystem |

You can use any of these commands instead of using the `mkfs` utility as a front end.

To create an ext2 filesystem on the first partition from the earlier example, you would issue the following command:

```
mkfs -t ext2 /dev/hda1 3686759
```

The notes you took while doing the partitioning are used here because you must provide the `mkfs` utility with the number of blocks on the partition you are formatting. If you did not note those numbers, you can rerun the `fdisk` command and display your partition table to find them.

When creating a filesystem, be very careful to ensure the device and block arguments are correct. If you designate the wrong device, you can destroy data on another partition. If you pass the wrong number of blocks, you might actually format part of another partition and destroy any data that is there.

The options you can use with the `mkfs` utility are listed in Table 3.4.

**Table 3.4** Options to Use with the `mkfs` Command

| Option | Action |
| :--- | :--- |
| `-t fs-type` | Defines the type of filesystem to create |
| `-v` | Displays all commands used to create the filesystem |
| `-c` | Checks for bad blocks before creating the filesystem |
| `-1 filename` | Uses the named file as a list of known bad blocks |

You also can use the `mkfs` command to create a filesystem on a floppy drive; however, the `fdformat` command is a better choice. It performs a low-level format to create the sector and track information on the floppy. The syntax for the `fdformat` command is as follows:

```
fdformat [option] device
```

You can use the `-n` option to prevent verification of the format. Floppy devices are usually `/dev/fd0` or `/dev/fd1`.

# Key Concept

> Before installing Linux, the disk must be prepared. You do this by creating your partitions, activating your swap partition, and designating the filesystem for each partition. After the partitions have been created, they must have a filesystem created by using the format command.
