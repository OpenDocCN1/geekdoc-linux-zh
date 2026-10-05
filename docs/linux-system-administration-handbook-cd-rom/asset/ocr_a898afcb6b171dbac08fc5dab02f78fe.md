# 10.8 Common Error Messages and What They Mean (Taken from the INN FAQ)

+   * SERVER cant remalloc xx bytes Cannot allocate memory

This error indicates that innd wanted to grow its data segment to a size larger than is allowed for a process. As limit the amount of space that the user can allocate (unlimit datasize) or rebuild the kernel with a larger max number of processes.

+   * Bad file number writing history file -- throttling

This error generally indicates that the news server hit the space limit for a given file. The news user must have a ulimit of 0 (infinite) to ensure that history and active files do not grow too large.

```
<article-id> 436 No space
```

This indicates that innd could not create a directory for a new newsgroup. This generally indicates that the section of the news pool that the new group creation was attempted in has the wrong permissions and/or ownership.

+   * File exists writing symlinking article file—throttling

This error happens when innd writes an article and then tries to symlink the crospost to another hierarchy in which the article ID it tries to use is already taken. This generally happens only if the active database and what exists on disk differ from one another or if an older version of Linux MMAP is being used. To solve the former, rebuild the active database. To solve the latter, rebuild INN with MMAP disabled.

+   * Not a directory writing article file—throttling

This indicates that there is a directory in the pool that innd thinks is a file. Normally this only happens after a crash and disk corruption when fsck guesses wrong the file type. To correct this, remove the offending file.

+   * Server throttled No space left on device writing article file

If this error occurs, either the machine is out of disk space or modes. To see how much space is used, execute "df -k"; to see the inode usage, execute "df -i.". If the machine is out of news, the newsmaster may want to consider rebuilding the partition to adjust the size of an inode and/or adjust the size values for the block/fragsize.