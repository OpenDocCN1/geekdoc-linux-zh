The previous command produces a wealth of information about the filesystem; just look for the following line:

```
Blocks per group:		8192
```

If a different number is given, use this number to locate the copies of the superblock. You can then tell the `e2fsck` command to use a copy of the superblock to check a partition you can't mount because of a corrupted superblock. So, if you can't mount a `/dev/hda1` that has an ext2 filesystem because of a corrupted superblock, issue the following:

```
e2fsck -f -b 16385 /dev/hda1
```

In the previous command, the `-f` option is used to force the check. If you do not use the `-f` option, `e2fsck` will look at the copy of the superblock and might think that the filesystem is clean. The `-b` option identifies the copy of the superblock that is to be used.

# ## Disk Usage

As files are created and saved to your system and log files are written to, your free disk space shrinks. It is important to monitor how much space is used on each disk. Linux runs best when there is adequate free space available.

To get optimal performance from your operating system, the amount of free space available should be 5–30 percent of each filesystem. In addition, if there is no free space, you will not be able to write to that filesystem.

Not only do you need to monitor the amount of free space, but you also will want to monitor what files are occupying the most space. By seeing what files are growing the fastest, or who is using the most space, you will be able to take steps to prevent your filesystem from becoming too full.

# ### du

The `du` command reports on the amount of space occupied by a single file or a directory and all its files and subdirectories. The syntax for the `du` command is as follows:

```
du [options] [filename]
```

In the previous syntax, `filename` can also be the name of a directory. If `du` is called without a filename, it will report on the working directory and its contents. Table 3.8 lists the options you can use with `du`.