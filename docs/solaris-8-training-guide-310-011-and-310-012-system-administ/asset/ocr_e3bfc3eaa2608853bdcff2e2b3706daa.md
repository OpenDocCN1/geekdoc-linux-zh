You define the fragment size when you create a UFS file system. The default fragment size is 1KB. Each block can be divided into one, two, four, or eight fragments, resulting in fragment sizes from 512 bytes to 8192 bytes (for 4KB file systems only). The lower boundary is actually tied to the disk sector size, typically 512 bytes.

When choosing a fragment size, look at the trade-off between time and space: A small fragment size saves space, but requires more time to allocate. As a general rule, a larger fragment size increases efficiency for file systems in which most of the files are large. Use a smaller fragment size for file systems in which most of the files are small.

> NOTE
The upper boundary might equal the full block size, in which case the fragment is not a fragment at all. This configuration might be optimal for file systems with large files when you are more concerned with speed than with space.

# Minimum Free Space

The minimum free space is the percentage of the total disk space held in reserve when you create the file system. Before Solaris 7, the default reserve was always 10%. In Solaris 7 and now Solaris 8, the minimum free space is automatically determined. This new method of calculating free space results in less wasted disk space on large file systems.

Free space is important because file access becomes less and less efficient as a file system gets full. As long as the amount of free space is adequate, UFS file systems operate efficiently. When a file system becomes full, using up the available user space, only root can access the reserved free space.

Commands such as df report the percentage of space available to users, excluding the percentage allocated as the minimum free space. When the command reports that more than 100% of the disk space in the file system is in use, some of the reserve has been used by root.

If you impose quotas on users, the amount of space available to the users does not include the free space reserve. You can change the value of the minimum free space for an existing file system by using the tunefs command.