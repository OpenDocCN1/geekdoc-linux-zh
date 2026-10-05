# Managing Filesystems
CHAPTER 18

options to the top-level mkfs (for example, -V to make it show what commands it executes
or -c to make it check the device for bad blocks). The generic mkfs program also enables
y to pass options to the filesystem-specific mkfs. Most of these filesystem-dependent
options sensible defaults, and usually do not want to change them. The only
options you might want to pass to mke2fs, which builds ext2 filesystems, are -m and -i.
M m specifies how much of the filesystem is reserved for root's use (for example,
for working space when the system disk would otherwise have filled completely). The -i
option is more rarely exercised and is used for setting the balance between inodes and disk
blocks; it is related to the expected average file size. As stated previously, the defaults are
reasonable for most purposes, these options are used only in special circumstances:

```
# mkfs -ext2 /dev/fd0
mke2fs 1.14, 9-Jan-99 for EXT2 FS 0.5b, 95/08/09
Linux ext2 filesystem format
Filesystem label=
360 inodes, 1440 blocks
72 blocks (5.00%) reserved for the super user
First data block=1
Block size=1024 (log=0)
Fragment size=1024 (log=0)
1 block group
8192 blocks per group, 8192 fragments per group
360 inodes per group
```

Writing inode tables: done
Writing superblocks and filesystem accounting information: done

```
# mount /floppy
# ls -la /floppy
total 14
drwx-xr-x 3 root root 1024 Sep 12 22:36 .
drwx-xr-x 20 root root 1024 Sep 10 04:38 -
drwx-xr-x 2 root root 12288 Sep 12 22:36 last+found
# umount /floppy
```

Here, you see the creating and mounting of an ext2 filesystem on a floppy. The structure
of the filesystem as specified by the program's defaults is shown. There is no volume
label, and there are 4,096 bytes (4KB) per inode (360x4=1,440). The block size is 1KB,
and 5 percent of the disk is reserved for root. These are the defaults (which are explained
in the manual page for mke2fs). After you you have created a filesystem, you can use
dumpe2fs to display information about an ext2 filesystem, but remember to pipe the result
through a pager as less because this output can be very long.

![](bbox=[0.845, 0.455, 0.943, 0.665])