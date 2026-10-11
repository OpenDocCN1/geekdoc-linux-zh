
## Filesystem Organization

Linux is organized in a hierarchical manner. It considers every file, directory, device, and link as a file that is placed on this structure. The most common organization for the directory structure is shown in Figure 3.2.

![](img/8dd1e68596303df43cb8ccf3197e8e53_75_0.png)

**Figure 3.2**
This figure shows a graphical representation of the organization of the Linux filesystem. This is independent of the actual partitions.

Each of the directories on the Linux filesystem conventionally contains certain types of files. Table 3.5 shows some of the more common directories and their contents.

**Table 3.5 Linux Directories and Their Contents**

| Directory | Contents |
|---|---|
| / | The beginning or root of the directory tree |
| /bin | Command binaries |
| /dev | Peripheral device files |
| /etc | Configuration files for the system |
| /home | Users’ home directories |
| /lib | Shared libraries |
| /mnt | Temporary partitions used for mounting |
| /proc | Virtual filesystem containing information about kernels and processes |
| /tmp | Application temporary files |
| /usr | Several subdirectories containing user commands, documentation, and other system information that does not change |
| /var | Log files and other files that change while the system is running |

### Inodes

The Linux operating system stores a lot of information about each file, including the following:

- Pointers to the file’s physical location on the disk
- The file’s name
- The file’s owner and group IDs
- Rules governing access to the file
- The file’s size
- The date and time the file was last accessed
- The date and time the file was last modified
- The date and time the inode was last modified
- The number of links to the file

A data structure called an inode is used to store the above information pertaining to each file with the exception of the file’s name. The file’s name is stored in its directory with an associated inode.

Each and every file has an inode associated with it. Even though every file can have more than one name through the use of links, each file has only one inode. (See Chapter 6, “Filesystem Organization," "Maintaining the Filesystem," for information on links.) Use `ls -i` to determine the number of the inode for any file. For example, issuing the command `ls -i MyFile` returns the following:

```
4144 MyFile
```

This means that the information about the file MyFile has an inode number of 4144. If an inode becomes corrupted, the file will no longer be accessible. Another way to see the inode number for a file is to use the stat command. Its syntax is

```
stat filename
```

Its output should look similar to the following:

```
File: 'mywhich'
Size: 101     Filetype: Regular File
Mode: (0775/-rwxrwxr-x)  Uid: ( 503/ hadden) Gid: ( 500/ hadden)
Device: 3,0   Inode: 147474  Links: 1
Access: Tue Oct 19 16:10:58 1999 (00019.19:52:38)
Modify: Fri May 28 09:02:47 1999 (00014.03:06:55)
Change: Fri Sep  3 17:20:37 1999 (00065.18:40:59)
```

The stat command reads the inode structure associated with the specified filename.

**Key Concept**

Each file has an associated inode that contains the file's physical location and all its attributes except for its filename. Use either the `ls -i` or stat command to determine a file's inode.

### File Types

Linux supports several file types and uses the first character in the permission block to name the file type. Linux does not differentiate between files and directories in the inode table. The operating system knows whether the file is a regular file or a directory by the file type character. The most common file type characters used by Linux are listed in Table 3.6.

**Table 3.6 The First Character of the Permission Block Identifies the File Type**

| Character | Type of File |
|-----------|--------------|
| -         | Ordinary file|
| b         | Block device |
| c         | Character device |
| d         | Directory |
| l         | Link |

Most files on the Linux system are ordinary files, including text files and applications. Any file a user creates is an ordinary file.

To Linux, directories are just empty files. They are organized in a hierarchical manner to provide holding places for other file types.

Block and character mode devices are composed of the instructions necessary for Linux to communicate with peripherals. These files are usually located in `/dev`.

Links are identified in the file type character as an l. See Chapter 6 for more information on links.

## Keeping Your Disks Healthy

After your partitions are created and formatted and you have installed Linux, you will want to make sure they stay healthy. You can use several different utilities to determine the state of your filesystem or fix problems with it.

### *fsck*

The most important utility for maintaining your filesystem is the **fsck** command. Like the **mkfs** command, **fsck** is a front end to the **check_disk** command for the specified filesystem type. It is used to verify the filesystem’s structure and repair any inconsistencies. Problems most frequently occur as a result of a system crash.

When a system crashes, the kernel is unable to sync the cache with the hard disk’s contents. This can result in blocks being marked as in use when they are really empty. Other errors can occur from directly writing to a device to an area containing existing data.

The syntax for the **fsck** command is

```
fsck -t fs-type device
```

For example, to check the first partition created as an ext2 filesystem in our earlier example, you would type the following:

```
fsck -t ext2 /dev/hda1
```

The previous command calls the **e2fsck** command to check the ext2 filesystem on the first partition of the first IDE hard disk. Because this is the root partition, you will receive a message that the filesystem is mounted and be asked whether to continue. If you answer yes, **fsck** checks the following:

- inodes
- blocks
- file sizes
- directory structure
- links

Any partition other than root can be unmounted while your system is running. To run the **fsck** command, you must first unmount that filesystem. See Chapter 6 for more information on mounting and unmounting file systems. To run **fsck** on your root partition, you can

- Start in read-only, single-user mode.
- Boot with a floppy and then scan the root partition.
- Run **fsck** during system boot.

When running **fsck** during system boot, the root filesystem is mounted in read-only mode, **fsck** runs, and then the root filesystem is mounted as read-write. All other filesystems are checked before they are mounted. Refer to Chapter 2, “Booting Linux,” for details on booting and passing parameters to your boot loader.

![](img/8dd1e68596303df43cb8ccf3197e8e53_79_0.png)

**Key Concept**

> The **fsck** command is used to verify the integrity of your filesystem. Unmount your filesystem before running it.

Options that are filesystem-specific for the **fsck** command are listed in Table 3.7.

**Table 3.7 fsck Options**

| Option | Action |
|---|---|
| -a | Causes **fsck** to run non-interactively |
| -c | Checks for bad blocks |
| -v | Reports on **fsck**'s progress |

The filesystem keeps information about the filesystem as a whole in the *superblock*. If the superblock becomes corrupted, the filesystem cannot be mounted; however, backup copies of it are spaced at regular intervals across the filesystem. By default, these copies are saved every 8,192 blocks. Because the first block is number 1 and not number 0, copies would be stored at block 8193, 16385, 24577, and so on. To verify that this is the block group size on your system, you can issue the following command:

```
dumpe2fs <device>
```

The previous command produces a wealth of information about the filesystem; just look for the following line:

```
Blocks per group: 8192
```

If a different number is given, use this number to locate the copies of the superblock. You can then tell the e2fsck command to use a copy of the superblock to check a partition you can't mount because of a corrupted superblock. So, if you can't mount a /dev/hda1 that has an ext2 filesystem because of a corrupted superblock, issue the following:

```
e2fsck -f -b 16385 /dev/hda1
```

In the previous command, the -f option is used to force the check. If you do not use the -f option, e2fsck will look at the copy of the superblock and might think that the filesystem is clean. The -b option identifies the copy of the superblock that is to be used.

### Disk Usage

As files are created and saved to your system and log files are written to, your free disk space shrinks. It is important to monitor how much space is used on each disk. Linux runs best when there is adequate free space available.

To get optimal performance from your operating system, the amount of free space available should be 5~30 percent of each filesystem. In addition, if there is no free space, you will not be able to write to that filesystem.

Not only do you need to monitor the amount of free space, but you also will want to monitor what files are occupying the most space. By seeing what files are growing the fastest, or who is using the most space, you will be able to take steps to prevent your filesystem from becoming too full.

### du

The du command reports on the amount of space occupied by a single file or a directory and all its files and subdirectories. The syntax for the du command is as follows:

```
du [options] [filename]
```

In the previous syntax, filename can also be the name of a directory. If du is called without a filename, it will report on the working directory and its contents. Table 3.8 lists the options you can use with du.
