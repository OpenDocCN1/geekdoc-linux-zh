# NOTE

The name **fsck** isn't the proper title for the ext2/ext3 repair tool; it's actually just a wrapper. The **fsck** wrapper tries to determine what kind of file system needs to be repaired and then runs the appropriate repair tool, passing any parameters that were passed to **fsck**. In ext2 and ext3, the real tool is called **e2fsck**. When a system crash occurs, you may need to call **e2fsck** directly rather than relying on other applications to call it for you automatically.

# Parameters Available for e2fsck

The parameters available for **e2fsck** are shown in Table 7-4.

For example, to run **e2fsck** on the /dev/hda3 file system, you would run:

```
[root@tedford /root]# e2fsck /dev/hda3
```

To force a check and automatically answer Yes to any prompts that come up, you would enter this command:

```
[root@tedford /]# e2fsck -f -y /dev/hda3
```

# TIP

You won't find an “e3fsck” command. The ext2 and ext3 file systems are so similar that the **e2fsck** command works on both of them.

| Parameter for e2fsck | Description |
| :--- | :--- |
| -b superblock | Specifies the superblock number from which **e2fsck** should read partition information. In most instances, **e2fsck** is able to find it at block 1, but if that block becomes corrupted, you'll need to specify an alternative number. Superblocks occur at every 8, 192 blocks, so the next superblock is at 8,193, then 16,385, and so on. |
| -c | Runs the **badblocks** program on the disk before running **e2fsck**. This searches the entire disk block-by-block and verifies the block's integrity. This is a very thorough way of checking a disk, but it is *extremely* time consuming. |
| -j journal | Sets the location of the external journal file, which is ordinarily hidden to avoid deletion and backup, which don't make sense for its contents. |
| -f | Forces a check to run even if it thinks the file system is already clean. |
| -y | Tells **e2fsck** to automatically assume that all prompts from **e2fsck** are to be answered Yes. |

Table 7-4 Options for the **e2fsck** Command