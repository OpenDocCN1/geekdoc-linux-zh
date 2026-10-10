![](bbox=[0.25, 0.1, 0.8, 0.37])

Figure 8-4 Fragmentation Is Our Friend

First, the entire disk is subdivided into uniform *disk blocks* (for the original UNIX file system, the block size was 512 bytes). A file’s data is stored in any available disk block. There is no requirement that they be sequential or contiguous. The disk’s free blocks are easily managed by the use of a simple bit allocation map. Each block is represented by a bit in the bitmap. If the bit is set, the block is in use; if it is not set, the block is available.

The challenge with this design is to track the specific blocks that belong to a file and the order in which they are allocated. To this end, a section of the disk space is reserved (at the time of file system creation) to hold information about each file (see Figure 8-5).