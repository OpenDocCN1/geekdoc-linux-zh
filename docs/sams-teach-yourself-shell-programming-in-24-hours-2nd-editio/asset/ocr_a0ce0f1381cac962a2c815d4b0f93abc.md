# -atime Is Often Defeated by Nightly Backups

In theory, find's -atime option is useful if you are short of disk space and want to find files that have not been accessed in a long time so that you can archive and delete them. However some backup programs, such as tar, prevent -atime from being useful because all files are accessed nightly during the system backup.

# find: -size Option

The -size option enables you to locate files based on the size of a file. It is useful when you want to find the largest files that are consuming disk space. Following -size, you must specify an integer number:

+   +n  Finds files that contain more than n blocks.
+   n  Finds files that contain exactly n blocks.
+   -n  Finds files that contain fewer than n blocks.

For example, the following command prints the name of all the files that are larger than 2,000 blocks:

```
find / -size +2000 -print
```

It is a very rare occasion when you need to search for files that contain an exact number of blocks. Usually you look for files that contain more than n blocks or fewer than n blocks. A common error is to forget the plus or minus sign for these types of find options and then wonder why find did not locate the expected files.

# What Is a Block?

A block is the smallest unit of the disk that can be allocated to a file. Although the size of the data in the file might be much less than the size of the block, it still takes up exactly one block on the disk.

The size of a block varies between systems. On BSD and Solaris systems the block size is usually 512 bytes. On Linux it is usually 1024 bytes.

# find: Combining Options

If you specify more than one option, the file must match all options to be displayed:

```
find / -name alpha -size +50 -mtime -3 -print
```