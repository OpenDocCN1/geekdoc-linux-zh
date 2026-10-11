verbose check of the first partition on the second IDE drive. The drive is marked clean, and the number of used files versus possible files and used blocks versus total blocks is shown.

```
# mount /fun
# fsck.ext2 -v /dev/hdb1
e2fsck 1.18, 11-Nov-1999 for EXT2 FS 0.5b, 95/08/09
/dev/hdb1: clean, 9692/1237888 files, 1754206/2474002 blocks
```

In the second example a check is **forcibly** forced on the same partition. The drive is carefully examined and more detailed information regarding files, links, and blocks is displayed.

```
# fsck.ext2 -v -f /dev/hdb1
e2fsck 1.18, 11-Nov-1999 for EXT2 FS 0.5b, 95/08/09
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information

9692 inodes used (0%)
157 non-contiguous inodes (1.6%)
# of inodes with ind/dind/tind blocks: 1194/205/0
1754206 blocks used (70%)
0 bad blocks

8884 regular files
776 directories
0 character device files
0 block device files
1 fifo
0 links
22 symbolic links (22 fast symbolic links)
0 sockets

9683 files

# mount /fun
```

When you’re finished checking the drive, you must mount it for it to be available for use by the system.

# du

The `du` utility is used to report the amount of disk space used by the files and subdirectory for the specified directory. If no directory is specified for the utility, `du` works with the `pwd`, or present working directory. The user must have read access to the files and directories in order for this utility to run. The function of the `du` utility can be controlled using a variety of options, which are covered in Table 5-9.