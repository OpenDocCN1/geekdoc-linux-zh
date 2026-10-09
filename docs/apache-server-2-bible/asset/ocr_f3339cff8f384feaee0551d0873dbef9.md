# # Changing the block size of the ext2 filesystem

One of the ways you can improve the ext2 file system’s performance is by changing the default block size from 1024 to a multiple of 1024 (usually less than 4096) for servers with mostly large files. To find out what kind of files you have on a particular ext2 partition do the following:

+   1. As root, change to the top directory of the ext2 partition.
+   2. Run the following commands, which really comprise a small script that uses the `find` and `awk` utilities. This command-line script will display all the files and their sizes and finally provide you with a total and average size of the entire partition.

```
find . -type f -exec ls -l {} \; | \\
awk 'BEGIN {tsize=0;fcnt=1;} \\
{ printf("%03d File: %6d size: %d bytes\n",fcnt++, $9,
$5); \\
tsize += $5;} \\
END { printf("Total size = %d\nAverage file size = %.02f\n",
tsize, tsize/fcnt);}'
```

+   3. After you know the average size of the file system, you can determine whether you should change the block size. If you discover that your average file size is 8192, which is $2 \times 4096$, you can change the block size to 4096.
+   4. Unfortunately, you cannot alter the block size of an existing ext2 file system without rebuilding it. So, you have to back up all your files from the file system and then rebuild the file system by using the `/sbin/mke2fs /dev/partition -b 4096` command. For example, if you have backed up the `/dev/hda7` partition and want to change the block size to 4096, use the `/sbin/mke2fs /dev/hda7 -b 4096` command.

Changing the block size to a higher number than the default (1024) may yield significant performance in raw read speed because of a reduced number of seeks and also because the `fsck` session during boot may be faster, because there may be less file fragmentation, and for other reasons. However, increasing the block size blindly (that is, without knowing the average file size) can result in wasted space. If the average file size is 2010 bytes on a system with 4096 byte blocks, each file will waste on an average 2086 bytes (4096 − 2010)! So know your file size before messing with the block size.

# # Tuning the ext2 file system with e2fsprogs

The default ext2 file system can be tuned using the e2fsprogs suite. In this section, I will discuss how you can install this suite of programs and use them in tuning, performing routine checks, and repairing your disks.