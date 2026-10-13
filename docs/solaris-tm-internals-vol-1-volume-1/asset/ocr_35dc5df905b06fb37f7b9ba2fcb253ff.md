+   - The first 12 direct blocks allow 12 blocks, or 98,304 bytes
+   - The first level of indirection allows a full file system block of disk addresses, which means that an 8-Kbyte block can hold 2,048 32-bit disk addresses; 12 + 2048 blocks, or (12 + 2048) × 8 = 1,687,520 bytes.
+   - The second level of indirection (double indirect) allows 12 + 2048 + (2048 × 2048) × 8KB = 34,376,613,888 bytes.

There is, however, a limit to the maximum offset in each disk address, which is expressed as a number of file system fragments; using the default fragments size of 1 Kbyte, the maximum offset for each block is 2^31 × 1KB = 2 terabytes.

# 14.2.6 UFS Block Allocation

UFS uses block sizes of 4 and 8 Kbytes, which provides significantly higher performance than the 512-byte blocks used in the System V file system. The downside of larger blocks was that when partially allocated blocks occurred, several kilobytes of disk space for each partly filled system block were wasted. To overcome this disadvantage, UFS uses the notion of file system fragments. Fragments allow a single block to be broken up into 2, 4, or 8 fragments when necessary.

UFS block allocation tries to prevent excessive disk seeking by attempting to co-locate inodes within a directory and by attempting to co-locate a file’s inode and its data blocks. Where possible, all of the inodes in a directory are allocated in the same cylinder group. This scheme helps reduce disk seeking when directories are traversed; for example, executing a simple ls -l of a directory will access all of the inodes in that directory. If all the inodes reside in the same cylinder group, most of the data will be cached after the first few files are accessed. A directory will be placed in a cylinder group different from that of its parent.

Blocks are allocated to a file sequentially, starting with the first 96 Kbytes (the first 12 direct blocks), skipping to the next cylinder group and allocating blocks up to the limit set by the file system parameter maxbgp, maximum-blocks-per-cylinder-group. After that, blocks are allocated from the next available cylinder group.

By default, on a file system greater than 1 Gbyte, the algorithm allocates 96 Kbytes in the first cylinder group, 16 Mbytes in the next available cylinder group, 16 Mbytes from the next, and so on. The maximum cylinder group size is 54 Mbytes, and the allocation algorithm only allows one-third of that space to be allocated to each section of a single file when it is extended. The maxbgp parameter is set to 2,048 8-Kbyte blocks by default at the time the file system is created; it is also tunable but can only be tuned downward, since the maximum cylinder group size is 16-Mbyte allocation per cylinder group.

Selection of a new cylinder group for the next segment of a file is governed by a rotor and free-space algorithm. A per-file-system allocation rotor points to one of the cylinder groups; each time new disk space is allocated, it starts with the cylinder group pointed to by the rotor. If the cylinder group has less than average free