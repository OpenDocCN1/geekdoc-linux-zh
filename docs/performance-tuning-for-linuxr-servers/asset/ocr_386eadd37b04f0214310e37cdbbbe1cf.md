+   The `-b block-size` option specifies the block size in bytes. Valid block size values are 1024, 2048, and 4096 bytes per block.
+   The `-n number-of-inodes` option specifies the number of inodes.
+   The `-t fs-type` option specifies how the file system will be used. The valid options are as follows:
+   
+   *   `news` creates one inode per 4KB block.
+   *   `largefile` creates one inode per megabyte.
+   *   `largefile4` creates one inode per 4 megabytes.

For a complete listing of the options to mkfs.ext2, see the mkfs.ext2 man page.

The following example uses the default when issuing `mkfs` on the device /dev/hdb2. The block size defaults to 4096, and the number of inodes created is 502944.

```
# mkfs.ext2 /dev/hdb2

mke2fs 1.32 (09-Nov-2002)
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
502944 inodes, 1004062 blocks
...
```

Next, set the block size to 1024 with the `-b 1024` option, and set the file system type with the `-T news` option. The number of inodes created is 1005568.

```
# mkfs -t ext2 -b 1024 -T news /dev/hdb2

mke2fs 1.32 (09-Nov-2002)
Filesystem label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
1005568 inodes, 4016250 blocks
...
```

# Ext3 Extensions for the Ext2 File System