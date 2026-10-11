The dmap control pages of the block allocation map contain a tree similar to the tree in a dmap structure, except that the leaf level contains 1024 elements. The dmap control page is defined by struct dmapctl_t which is found in the linux\include\linux\JFS\JFS_dmap.h.

At the top of the block allocation map there is a map control structure, struct dbmap_t. This structure contains summary information that speeds up the finding of AGs which have more-than-average free space. This structure is found in the linux\include\linux\JFS\JFS_dmap.h.

The block allocation map is not journaled: it can be repaired during recovery time by logredo, or reconstructed by fsck.

# # Inode Allocation Map

The inode allocation map solves the forward lookup problem. The aggregate and each filesset maintain an inode allocation map, which is a dynamic array of *inode allocation groups* (IAGs). The IAG is the data for the inode allocation map. For the aggregate, the inodes mapped by the inode allocation map are also known as the *aggregate inode table*. For a filesset, the inodes mapped by the inode allocation map are also known as the *file inode table*.

Each IAG is 4K in size and describes 128 physical inode extents on the disk. Because each inode extent contains 32 inodes, each IAG describes 4,096 inodes. An IAG can exist anywhere in the aggregate. All of the inode extents for an IAG exist in one allocation group. The IAG is tied to that aggregate group (AG) until all of its inode extents are freed. At that point an inode extent could be allocated for it in any AG, and then the IAG would be tied to that AG. The IAG is defined by the *iag_t* structure, which is found in the file *linux\include\linux\JFS\JFS_omap.h*.

The first 4K page of the inode allocation map is a control page. This page contains summary information for the inode allocation map. The definition for the *dinomap_t* structure is found in the *linux\include\linux\JFS\JFS_omap.h* file.

Abstractly, the inode allocation map is a dynamically extensible array of the IAG structures: *struct iag inode_allocation_map \[1..N\]*. Physically, the inode allocation map is itself a file within the aggregate. The aggregate inode allocation map is described by the aggregate self-node.

The filesset inode allocation map is described by *Filesset_Inode*. Its pages are allocated and freed as necessary under standard B+tree indexing. The key for the B+tree is the byte offset of the IAG page.