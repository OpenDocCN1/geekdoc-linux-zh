# SOLARIS FILE SYSTEM CACHE

One of the most important features of a file system is its ability to cache file data, but ironically, the file system cache is not implemented in the file system. In Solaris, the file system cache is implemented in the virtual memory system. In this section, we explain how Solaris file caching works, and we explore the interactions between the file system cache and the virtual memory system.

# 15.1 Introduction to File Caching

Traditional Unix implements file system caching in the I/O subsystem by keeping copies of recently read or written blocks in a block cache. This block cache sits just above the disks, and it caches data corresponding to physical disk sectors.

Figure 15.1 shows an example in which a process reads a piece of a file by issuing a read system call into the operating system. The file system must then look up the corresponding disk block for the file by looking up the block number in the direct/indirect blocks for that file, after which the file system requests the block from the I/O system. The I/O system retrieves the block from disk the first time; then, the file systems satisfies subsequent reads by reading the disk block from the buffer cache. Note that even though the disk block is cached in memory—because this is a physical block cache—we have to invoke the file system and look up the physical block number for every cached read.