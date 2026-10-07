# 14.2.7 UFS Allocation and Parameters

Figure 14.6 shows the default allocation that is used if a file is created on a large UFS. The first 96 Kbytes of file 1 are allocated from the first cylinder group. Then, allocation skips to the second cylinder group and another 16 Mbytes of file 1 are allocated, and so on. When another file is created, we can see that it consumes the holes in the allocated blocks alongside file 1. There is room for a third file to do the same.

![](bbox=[0.173, 0.276, 0.958, 0.523])

Figure 14.6 Default File Allocation in 16-Mbyte Groups

The actual on-disk layout will not be as simple as the example shown reflects the allocation policies discussed. We can use an add-on tool, filestat, to view the on-disk layout of a file, as shown below.

```
# /usr/local/bin/filestat testfile
odes per cyl group: 128
odes per block: 64
cylinder Group no: 0
cylinder Group blk: 64
File System Block Size: 8192
Block Size: 512
Number of 512b Blocks: 262288

Start Block      End Block      Length (512 byte Blocks)
144 -> 335       192
400 -> 33167       32768
110800 -> 143567      32768
221264 -> 221343      80
221216 -> 221263      48
224156 -> 254095      32640
331856 -> 331999      144
331808 -> 331855      48
332112 -> 364687      32576
442448 -> 442655      208
442400 -> 442447      48
442768 -> 475279      32512
```