Notice from the preceding output that the `fsck` command does not give lengthy output on the terminal screen when checking the file system; this is because the `fsck` command only performs a quick check for errors unless the `-f` option is used to perform a full check, as shown in the following example:

```
```
[root@server1 root]# fsck -f -t ext2 /dev/fd0
fsck 1.35 (28-Feb-2004)
e2fsck 1.35 (28-Feb-2004)
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
/dev/fd0: 14/184 files (0.0% non-contiguous), 45/1440 blocks
[root@server1 root]#
```
```

Table 6-6 displays a list of common options used with the `fsck` command.

| **Table 6-6 Common options to the `fsck` command** |
| --- |
| **Option** | **Description** |
| -f | Performs a full filesystem check |
| -a | Allows fsck to automatically repair any errors |
| -A | Checks all file systems in /etc/fstab that have a 1 or 2 in the sixth field |
| -Cf | Performs a full filesystem check and displays a progress line |
| -AR | Checks all file systems in /etc/fstab that have a 1 or 2 in the sixth field but skips the / filesystem |
| -V | Displays verbose output |

If the `fsck` command finds a corrupted file, it displays a message to the user asking whether to fix the error; to avoid these messages, you may use the `-a` option listed in Table 6-6 to specify that the `fsck` command should automatically repair any corruption. If there are files that the `fsck` command cannot repair, it places them in the lost+found directory on that file system and renames the file to the inode number.

To view the contents of the lost+found directory, simply mount the device and view the contents of the lost+found directory immediately under that mount point. Because it is difficult to identify lost files by their inode number, most users delete the contents of this directory periodically. Recall that the lost+found directory is automatically created when an ext2 or ext3 file system is created by the `mkfs` command.