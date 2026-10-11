A solution to this problem is provided by the ReiserFS format, which organizes data in a different way. This file system format has currently a fixed block size of 4096 bytes.

However, small files are stored more efficiently. Only as much space is reserved as is actually required—not an entire block. Small files or the ends of files are stored together in the same block.

The inodes required are not generated when the file system is created, but only when they are actually needed. This allows a more flexible solution to storage requirements, increasing efficiency in the use of hard drive space.

Another advantage of the ReiserFS is that access to files is quicker. This is done through the use of balanced binary trees in the organization of data blocks.

However, balanced trees require considerably more processing power because after every file is written the entire tree must be rebalanced.

The current version of the ReiserFS (3.6) contained in the kernel since version 2.4.x allows a maximum partition size of 16 TB. A file also has a maximum size of 16 TB.

The same limitations exist for filenames as with the ext2 file system format.

# ### Directories

Inodes contain all the administrative information for a file, but not the filename. The filename is stored in the directory.

Like a catalog, directories contain information on other files. This information includes the number of the inode for the file and its name.

**1 HARDCOPY PERMITTED-NO DISTRIBUTION ALLOWED**