Other useful file system management utilities include the following:

+   - `tune2fs` This utility is used to adjust various file system parameters on ext2/3/4 file systems. These are some of the options you can use:

+   - `-c n` Sets the number of mounts (*n*) after which the filesystem will automatically be checked by fsck.

+   - `-i interval d| m| w` Sets the maximum time between file system checks in d (days), m (months), or w (weeks).

+   - `-j` Adds a journal to an ext2 file system.

+   - `-L volume_label` Sets the volume label of the filesystem.

Here is an example:

```
```bash
ws1:/ # tune2fs -L NewVol /dev/sdb1
tune2fs 1.41.11 (14-Mar-2010)
ws1:/ #
```
```

+   - `reiserfstune` This is the Reiser equivalent of the tune2fs utility.

+   - `dumpe2fs` Displays lots of useful information about ext2/3/4 file systems. Use the `-h` option to make the output more readable. An example follows:

```
```bash
ws1:/ # dumpe2fs -h /dev/sdb1
dumpe2fs 1.41.11 (14-Mar-2010)
Filesystem volume name:  NewVol
Last mounted on:		/mnt/extra space
Filesystem UUID: 95b5b6cc-19aa-49fe-972a-9a1f734906b0
Filesystem magic number:	0x38655
Filesystem revision #: 1 (dynamic)
Filesystem features: has_journal ext_attr resize_inode dir_index filetype extent flex_bg sparse_super large_file huge_file unix_flags extra_isize
Default mount options: (none)
Filesystem state:  clean
Errors behavior: Continue
Filesystem OS type:  Linux
Inode count: 402192
Block count: 1605632
Reserved block count: 80324
Free blocks: 1544479
Free inodes: 402180
First block: 0
Block size: 4096
Fragment size: 4096
Reserved GDT blocks: 391
Blocks per group: 32768
Fragments per group: 32768
Inodes per group: 8208
Inode blocks per group: 513
Flex block group size: 16
Filesystem created: Wed Mar 16 11:50:04 2011
Last mount time: Wed Mar 16 14:27:42 2011
Last write time: Wed Mar 16 14:49:50 2011
Mount count: 2
```
```