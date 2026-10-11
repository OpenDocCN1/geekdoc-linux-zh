`mkfs` is the front end to each file system's format program and its subprograms. `mkfs` creates file systems on disk partitions (or volumes, if a volume manager is being used).

The `mkfs` command can usually run without the optional parameters that affect performance. To a large degree, this is because the default parameters are adequate in most cases. `mkfs` calculates the appropriate parameters to use based on the information it can ascertain about the volume or disk drive, and then it calls the file system `mkfs` command to actually create the file system.

# ## Basic File System Terms

Before delving any further into file systems on Linux, it's important to learn some of the common file system terms. These terms are used throughout the remainder of this chapter.

+   - A **_logical block_** is the smallest unit of storage that can be allocated by the file system. A logical block is measured in bytes, and it may take several blocks to store a single file.

+   - A **_logical volume_** can be one or more physical disks or some subset of the physical disk space.

+   - **_Block allocation_** is a method of allocating blocks where the file system allocates one block at a time. In this method, a pointer to every block in a file is maintained and recorded. Ext2 uses block allocation.

+   - **_Extent allocation. Large_** numbers of contiguous blocks, called extents, are allocated to the file and are tracked as a unit. A pointer needs only to be maintained to the beginning of the extent. Because a single pointer is used to track a large number of blocks, the bookkeeping for large files is much more efficient.

+   - **_Fragmentation_** is the scattering of files into blocks that are not contiguous and is a problem that all file systems encounter. Fragmentation is caused when files are created and deleted. The fragmentation problem can be solved by having the file system use advanced algorithms to reduce fragmentation.

+   - **_Internal fragmentation_** occurs when a file does not a fill a block completely. For example, if a file is 10K and a block is 8K, the file system allocates two blocks to hold the file, but 6K is wasted. Notice that as blocks get bigger, so does the waste.

+   - **_External fragmentation_** occurs when the logical blocks that make up a file are scattered all over the disk. External fragmentation can cause poor performance.