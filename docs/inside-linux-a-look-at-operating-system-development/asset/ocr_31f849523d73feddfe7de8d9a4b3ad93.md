routines to perform details which vary from one file system implementation to another.

![](bbox=[0.28, 0.18, 0.72, 0.42])

Figure 5.20: File system layers

This, and other indirection inside the kernel file system code, becomes the “virtual file system”.

The utility of this is the ease with which new file system implementations can be added to the kernel. The only time the file system type is visible is when a partition is mounted. Thereafter, the file system specific code is accessed indirectly through pointers in inodes. This hierarchy is suggested in Figure 5.20.

# The open call

The `open` call turns a pathname<sup>10</sup> and access arguments into a file descriptor, a small, non-negative integer which is used as an argument to the other I/O calls. This is done in two steps.

The `namei` function within the kernel first takes the leading part of the file pathname and returns the inode of the parent directory. (If that directory cannot be located, the open fails.) If the pathname starts with “/”, the search is started from the inode noted as that process’ root directory, if not, the inode noted as the current working directory is used as the starting point.

<sup>10</sup> This is the *entire* file name, including any leading directories, not just the root part.