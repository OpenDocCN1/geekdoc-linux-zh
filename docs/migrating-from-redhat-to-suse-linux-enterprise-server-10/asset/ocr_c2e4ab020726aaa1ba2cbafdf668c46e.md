A possible problem in the ext2 (or ext3) file system is damage to the superblock. You can first view the location of all copies of the superblock in the file system using **dumpext2fs**.

Then, with **e2fsck**, you can use one of the backup copies, as in the following:

```
```
e2fsck -f -b 32768 /dev/hda1
```
```

In this example, the superblock located at data block 32768 in the ext2 file system of the partition /dev/hda1 is used and the primary superblock is updated appropriately upon completion of the file system check.

> > With a block size of 4k, a backup copy of the superblock is stored every 32768 blocks.

With **reiserfsck**, the file system is subjected to a consistency check. The journal is checked to see if certain transactions need to be repeated. With the option --**fix-fixable**, errors such as wrong file sizes are fixed as soon as the file system is checked.

With an error in the binary tree, it is possible to have this rebuilt by entering **reiserfsck --rebuild-tree**.

# ### Use Additional Tools to Manage File Systems

There are additional tools to administer various aspects of file systems.

**tune2fs** is used to adjust tunable filesystem parameters on ext2/ext3 file systems. Amongst these is the number of days or number of mounts a file system check is done. It is also used to add a label to the file system, or to add a journal to an ext2 file system, turning it into an ext3 file system.