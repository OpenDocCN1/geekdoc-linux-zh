| Option | Description |
| :--- | :--- |
| -f | Performs a full filesystem check |
| -a or -y | Allows `fsck` to automatically repair any errors |
| -A | Checks all filesystems in `/etc/fstab` that have a 1 or 2 in the sixth field |
| -Cf | Performs a full filesystem check and displays a progress line |
| -AR | Checks all filesystems in `/etc/fstab` that have a 1 or 2 in the sixth field but skips the / filesystem |
| -V | Displays verbose output |

**Table 5-6 Common options to the fsck Command**

To view the contents of the lost+found directory, simply mount the device and view the contents of the lost+found directory immediately underneath the mount point. Because it is difficult to identify lost files by their inode number, most users delete the contents of this directory periodically. Recall that the lost+found directory is automatically created when an ext2, ext3 or ext4 filesystem is created.

Just as you can use the `mkfs` command to make an ext2, ext3, or ext4 filesystem, you can use the `e2fsck` command to check an ext2, ext3, or ext4 filesystem. The `e2fsck` command accepts more options and can check a filesystem more thoroughly than `fsck`. For example, by using the `-c` option to the `e2fsck` command, you can check for bad blocks on the hard disk and add them to a bad block table on the filesystem so that they are not used in the future, as shown in the following example:

```
```
[root@server1 ~]# e2fsack -c /dev/vg00/data
e2fsck 1.42.8 (20-Jun-2013)
Checking for bad blocks (read-only test): done
/dev/vg00/data: Updating bad block inode.
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
/dev/vg00/data: ***** FILE SYSTEM MODIFIED *****
/dev/vg00/data: 11/983040 files (0.0% non-contiguous), 104064/3932160 blocks
[root@server1 ~]# _
```
```

![](bbox=[0.17, 0.8, 0.29, 0.89])

The badblocks command can be used to perform the same function as the `e2fsck` command with the `-c` option.

You cannot use the `fsck` command to check a btrfs filesystem. Instead, you must use the **btrfs command** to check a btrfs filesystem after unmounting it. For example, the command `btrfs check /dev/sda5` will check the unmounted btrfs filesystem on `/dev/sda5`.