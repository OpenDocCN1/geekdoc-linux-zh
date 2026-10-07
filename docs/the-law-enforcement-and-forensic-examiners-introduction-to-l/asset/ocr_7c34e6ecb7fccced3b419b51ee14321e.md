# v.4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

are now running the commands on the original dd image. We'll continue on the sake of completeness. And because it's good practice...

```
barry@forensic1:~/able2$ blkstat -o 10260 able2.dd 5184
Fragment: 5184
Not Allocated
Group: 0
```

Using the command blkcat we can look at the raw contents of the data block (using xdd and as a viewer). If we want, we can use even blkcat to extract the block, redirecting the contents to another file, just as we did in exercise #2B with our ext4 file system image.

If we want to recover the actual file and meta data associated with the identified data block, we use find to determine which meta data structure (in this case since we are working on an EXT file system) holds the data in block 5184. And istat shows us the meta data for the node:

```
barry@forensic1:~/able2$ find -o 10260 -d 5184 able2.dd
10090
```

```
barry@forensic1:~/able2$ istat -o 10260 able2.dd 10090
inode: 10090
Not Allocated
Group: 5
Generation Id: 3534950782
uid / gid: 4 / 7
mode: rw-r---
size: 3591
num of links: 0
```

```
Inode Times:
Accessed: 2003-08-10 00:18:36 (EDT)
File Modified: 1996-12-25 16:27:43 (EST)
Inode Modified: 2003-08-10 00:29:58 (EDT)
Deleted: 2003-08-10 00:29:58 (EDT)
```

```
Direct Blocks:
5184 5185 5186 5187
```

Again, as we saw previously, the istat command, which shows us the meta data for inode 10090, indicates that the file with this node is Not Allocated, and its first direct block is 5184. Just as we expected.

241