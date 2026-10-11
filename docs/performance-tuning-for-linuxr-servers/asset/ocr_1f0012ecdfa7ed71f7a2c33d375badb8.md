# # XFS File Layout

The `xfs_db` enables the examination of XFS file system structures. The `xfs_db` utility takes the device as the parameter. The `xfs_db` man page contains information about how to display the data structures for XFS.

This section shows how to display an inode on an XFS system.

The XFS file system is on the device /dev/hda5.

```
```bash
# mount -t xfs /dev/hda5 /xfs
# cd /xfs
```
```

Copy the fstab file located in the /etc directory onto the XFS file system.

```
```bash
# cp /etc/fstab .
# ls all
```
```

```
```text
total 12
drwxr-xr-x   2 root root     18 Dec  8 10:57 .
drwxr-xr-x   24 root root   4096 Dec  8 10:54 ..
-rw-r--   1 root root   948 Dec  8 10:57 fstab
```
```

To look at a file's inode, its inode number is required. Use the `ls` command with the `--` option to determine this number. In the following example, the inode number for the fstab file is 131.

```
```bash
# ls i
    128 .       2 ..        131 fstab
# cd ..
# umount /xfs
```
```

The `xfs_db` option to look at an inode is the `inode` command. The `inode` command uses the inode number as the parameter. To print the file system information about the inode, use the `p` command.

```
```bash
# xfs_db /dev/hda5
     xfs_db> inode 131
     xfs_db> p
core.magic = 0x494e
core.mode = 0100644
core.version = 1
core.format = 2 (extents)
core.nlinkvl = 1
core.uid = 0
core.gid = 0
```
```