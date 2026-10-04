The ability to allocate fragments of blocks to files, rather than just whole blocks, saves space by reducing fragmentation of disk space resulting from unused holes in blocks.

You define the fragment size when you create a UFS file system. The default fragment size is 1KB. Each block can be divided into 1, 2, 4, or 8 fragments, resulting in fragment sizes from 8,192 bytes to 512 bytes (for 4KB file systems only). The lower bound is actually tied to the disk sector size, typically 512 bytes.

> NOTE. The upper bound might equal the full block size, in which case the fragment is not a fragment at all. This configuration might be optimal for file systems with very large files when you are more concerned with speed than with space.

When choosing a fragment size, look at the trade-off between time and space: a small fragment size saves space but requires more time to allocate. As a general rule, a larger fragment size increases efficiency for file systems in which most of the files are large. Use a smaller fragment size for file systems in which most of the files are small.

# Minimum Free Space

The minimum free space is the percentage of the total disk space held in reserve when you create the file system. The default reserve is 10%. Free space is important because file access becomes less and less efficient as a file system gets full. As long as there is an adequate amount of free space, UFS file systems operate efficiently. When a file system becomes full, using up the available user space, only root can access the reserved free space.

Commands such as df report the percentage of space available to users, excluding the percentage allocated as the minimum free space. When the command reports that more than 100% of the disk space in the file system is in use, some of the reserve has been used by root.

If you impose quotas on users, the amount of space available to the users does not include the free space reserve. You can change the value of the minimum free space for an existing file system by using the tunefs command.

# Rotational Delay (Gap)

The rotational delay is the expected minimum time (in milliseconds) it takes the CPU to complete a data transfer and initiate a new data transfer on the same disk cylinder. The default delay depends on the type of disk and is usually optimized for each disk type.

When writing a file, the UFS allocation routines try to position new blocks on the same disk cylinder as the previous block in the same file. The allocation routines also try to optimally position new blocks within tracks to minimize the disk rotation needed to access them.