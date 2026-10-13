# 14.2.7 UFS Allocation and Parameters

space, then it is skipped and the next cylinder group is tried. This algorithm makes the file system attempt to balance the allocation across the cylinder groups.

Figure 0.1 shows the default allocation that is used if a file is created on a large UFS. The first 96 Kbytes of file 1 are allocated from the first cylinder group. Then, allocation skips to the second cylinder group and another 16 Mbytes of file 1 are allocated, and so on. When another file is created, we can see that it consumes the holes in the allocated blocks alongside file 1. There is room for a third file to do the same.

![](bbox=[0.1649, 0.3251, 0.9161, 0.56])

**Figure 0.1** *Default File Allocation in 16-Mbyte Groups*