Any partition other than root can be unmounted while your system is running. To run the fsck command, you must first unmount that filesystem. See Chapter 6 for more information on mounting and unmounting filesystems. To run fsck on your root partition, you can

+   □ Start in read-only, single-user mode.
+   □ Boot with a floppy and then scan the root partition.
+   □ Run fsck during system boot.

When running fsck during system boot, the root filesystem is mounted in read-only mode, fsck runs, and then the root filesystem is mounted as read-write. All other filesystems are checked before they are mounted. Refer to Chapter 2, “Booting Linux,” for details on booting and passing parameters to your boot loader.

![](bbox=[0.15, 0.375, 0.2, 0.42])

# Key Concept

> The fsck command is used to verify the integrity of your filesystem. Unmount your filesystem before running it.

Options that are filesystem-specific for the fsck command are listed in Table 3.7.

| Table 3.7 The Filesystem-Specific fsck Options and Their Actions | | | | | | | |
|---|---|---|---|---|---|---|---|
| | *Option* | | | | | | *Action* | | | | | | | |
| | -a | | | | | | Causes fsck to run non-interactively | | | | | | | |
| | -c | | | | | | Checks for bad blocks | | | | | | | |
| | -v | | | | | | Reports on fsck’s progress | | | | | | | |

The filesystem keeps information about the filesystem as a whole in the superblock. If the superblock becomes corrupted, the filesystem cannot be mounted; however, backup copies of it are spaced at regular intervals across the filesystem. By default, these copies are saved every 8,192 blocks. Because the first block is number 1 and not number 0, copies would be stored at block 8193, 16385, 24577, and so on. To verify that this is the block group size on your system, you can issue the following command:

```
dumpe2fs device
```