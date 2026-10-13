The mkfs utility builds an ext2 type filesystem by default. The results of running mkfs are reported as follows:

```
```text
# mkfs /dev/hdb2
mke2fs 1.10, 24-Apr-97 for EXT2 FS 0.5b, 95/08/09
Linux ext2 filesystem format
Filesystem label=
3024 inodes, 12096 blocks
604 blocks (4.99%) reserved for the super user
First data block=1
Block size=1024 (log=0)
Fragment size=1024 (log=0)
2 block groups
8192 blocks per group, 8192 fragments per group
1512 inodes per group
Superblock backups stored on blocks:
    8193
Writing inode tables: done
Writing superblocks and filesystem accounting information: done
```
```

If you are installing an older hard drive, I strongly recommend that you use the -c option to check for bad blocks, as in the following example:

```
```text
# mkfs -c /dev/hdb2
mke2fs 1.10, 24-Apr-97 for EXT2 FS 0.5b, 95/08/09
Linux ext2 filesystem format
Filesystem label=
3024 inodes, 12096 blocks
604 blocks (4.99%) reserved for the super user
First data block=1
Block size=1024 (log=0)
Fragment size=1024 (log=0)
2 block groups
8192 blocks per group, 8192 fragments per group
1512 inodes per group
Superblock backups stored on blocks:
    8193 ....

Checking for bad blocks (read-only test): done
Writing inode tables: done
Writing superblocks and filesystem accounting information: done
```
```

When an ext2 filesystem is created, it builds a set of areas on the hard drive partition. These areas are commonly referred to as block groups. Each block group is segmented into several smaller sections. Figure 9.1 depicts the block group layout, and Table 9.4 describes each of the sections of a block group.

| Block Group Section | Description |
|---|---|
| Superblock | Information about the entire filesystem is stored in the superblock. Each block group contains a superblock, but it is only a backup copy of the superblock in the first block group. |