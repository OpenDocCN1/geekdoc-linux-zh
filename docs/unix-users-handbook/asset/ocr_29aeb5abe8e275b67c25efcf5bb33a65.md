# # df

**df - Report the amount of free disk blocks.**

![](bbox=[0.88, 0.11, 0.97, 0.2])

```
df (1M)                                            df (1M)
```

# NAME

df (generic) - report number of free file system disk blocks

# SYNOPSIS

```
/usr/bin/df [-F FSType] [-befgiklnv] [-t|-P] [-o specific_options] [-V] [special|directory]...
```

# DESCRIPTION

The df command displays the number of free 512-byte blocks and free inodes available for file systems by examining the counts kept in the superblock or superblocks. If a special or a directory is not specified, the free space on all mounted file systems is displayed. If the arguments to df are path names, df reports on the file systems containing the named files. If the argument to df is a special of an unmounted file system, the free space in the unmounted file system is displayed.

df recognizes the following options:

+   -   **-b** Report only the number of kilobytes (KB) free.
-   **-e** Report the number of files free.
-   **-f** Report only the actual count of the blocks in the free list (free inodes are not reported).
-   **-F FSType** Report only on the FSType file system type (see fstyp(1M)).
-   **-g** Report the entire structure described in statvfs(2).
-   **-i** Report the total number of inodes, the number of free inodes, number of used inodes, and the percentage of inodes in use.
-   **-k** Report the allocation in kilobytes (KB).
-   **-l** Report on local file systems only.
-   **-n** Report the file system name. If used with no other options, display a list of mounted file system types.
-   **-o specific_options** Specify options specific to each file system type. specific_options is a comma-separated list of suboptions intended for a specific Fstype module