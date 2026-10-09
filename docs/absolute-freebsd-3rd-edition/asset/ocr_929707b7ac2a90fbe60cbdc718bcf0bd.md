machines. I discuss choosing a filesystem in Chapter 2.

# ## UFS Components

UFS is built of two layers, one called the *Unix File System* and the other the *Fast File System* (FFS). UFS handles items like filenames, attaching files to directories, permissions, and all of those petty details users care about. FFS does the real work in getting files written to disk and arranging them for quick access. The two work together to provide data storage.

# ### The Fast File System

FFS is built of superblocks, blocks, fragments, and inodes.

A *superblock* records the filesystem’s characteristics. It contains a magic number that identifies the filesystem as UFS, as well as filesystem geometry information the kernel uses to optimize writing and reading files. A UFS filesystem keeps many backup copies of the superblock, in case the primary gets damaged.

*Blocks* are segments of disk that contain data. FreeBSD defaults to 32KB blocks. FFS maps blocks onto specific sectors on the underlying disk or GEOM provider. Every stored file gets broken up into 32KB chunks, and each chunk is stored in its own block.

Not all files are even multiples of 32KB, so FFS stores the leftovers in *fragments*. The standard is one-eighth of the block size, or 4KB. For example, a 39KB file would fill one block and two fragments. One of those fragments has only 3KB in it, so fragments do waste disk space—but they waste far less space than using full blocks everywhere.

# ### How UFS Uses FFS

UFS allocates certain FFS blocks as *inodes*, or *index nodes*, to map blocks and fragments to files. An inode contains each file’s size, permissions, and the list of blocks and fragments containing each file. Collectively, the data in an inode is known as *metadata*, or data about data.