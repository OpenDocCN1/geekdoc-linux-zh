
sensitive; getting every last drop out of your hard disk is much more important than squeezing an extra percent of speed out of your keyboard. Furthermore, as you will see, the complexity of block devices provides a lot of room for such optimizations. The topic of this chapter is how the kernel manages block devices and their requests. This part of the kernel is known as the block I/O layer. Interestingly, revamped the block I/O layer was the primary goal for the 2.5 development kernel. This chapter covers the all-new block I/O layer in the 2.6 kernel.

## Anatomy of a Block Device

The smallest addressable unit on a block device is a sector. Sectors come in various powers of two, but 512 bytes is the most common size. The sector size is a physical property of the device, and the sector is the fundamental unit of all block devices—the device cannot address or operate on a unit smaller than the sector, although many block devices can operate on multiple sectors at one time. Most block devices have 512-byte sectors, although other sizes are common. For example, many CD-ROM discs have 2-kilobyte sectors.

Software has different goals and therefore imposes its own smallest logically addressable unit, which is the block. The block is an abstraction of the filesystem—filesystems can be accessed only in multiples of a block. Although the physical device is addressable at the sector level, the kernel performs all disk operations in terms of blocks. Because the device’s smallest addressable unit is the sector, the block size can be no smaller than the sector and must be a multiple of a sector. Furthermore, the kernel (as with hardware and the sector) needs the block to be a power of two. The kernel also requires that a block be no larger than the page size (see Chapter 12, “Memory Management,” and Chapter 19, “Portability”).¹ Therefore, block sizes are a power-of-two multiple of the sector size and are not greater than the page size. Common block sizes are 512 bytes, 1 kilobyte, and 4 kilobytes.

Somewhat confusingly, some people refer to sectors and blocks with different names. Sectors, the smallest addressable unit to the device, are sometimes called “hard sectors” or “device blocks.” Meanwhile, blocks, the smallest addressable unit to the filesystem, are sometimes referred to as “filesystem blocks” or “I/O blocks.” This chapter continues to call the two notions sectors and blocks, but you should keep these other terms in mind. Figure 14.1 is a diagram of the relationship between sectors and buffers.

Other terminology, at least with respect to hard disks, is common—terms such as clusters, cylinders, and heads. Those notions are specific only to certain block devices and, for the most part, are invisible to user-space software. The reason that the sector is important to the kernel is because all device I/O must be done in units of sectors. In turn, the higher-level concept used by the kernel—blocks—is built on top of sectors.

> ¹ This is an artificial constraint that could go away in the future. Forcing the block to remain equal to or smaller than the page size, however, simplifies the kernel.

![](img/48bc90306f7476ca73ca7a99267ff690_317_0.png)

## Buffers and Buffer Heads

When a block is stored in memory—say, after a read or pending a write—it is stored in a buffer. Each buffer is associated with exactly one block. The buffer serves as the object that represents a disk block in memory. Recall that a block is composed of one or more sectors but is no more than a page in size. Therefore, a single page can hold one or more blocks in memory. Because the kernel requires some associated control information to accompany the data (such as from which block device and which specific block the buffer is), each buffer is associated with a descriptor. The descriptor is called a *buffer head* and is of type `struct buffer_head`. The *buffer* head structure holds all the information that the kernel needs to manipulate buffers and is defined in `<linux/buffer_head.h>`.

Take a look at this structure, with comments describing each field:

```c
struct buffer_head {
    unsigned long b_state;      /* buffer state flags */
    struct buffer_head *b_this_page; /* list of page's buffers */
    struct page *b_page;        /* associated page */
    sector_t b_blocknr;         /* starting block number */
    size_t b_size;              /* size of mapping */
    char *b_data;               /* pointer to data within the page */
    struct block_device *b_bdev; /* associated block device */
    bh_end_io_t *b_end_io;      /* I/O completion */
    void *b_private;            /* reserved for b_end_io */
    struct list_head b_assoc_buffers; /* associated mappings */
    struct address_space *b_assoc_map; /* associated address space */
    atomic_t b_count;           /* use count */
};
```

The `b_state` field specifies the state of this particular buffer. It can be one or more of the flags in Table 14.1. The legal flags are stored in the `bh_state_bits` enumeration, which is defined in `<linux/buffer_head.h>`.

Table 14.1  `bh_state` Flags

| Status Flag | Meaning |
| :--- | :--- |
| BH_Uptodate | Buffer contains valid data. |
| BH_Dirty | Buffer is dirty. (The contents of the buffer are newer than the contents of the block on disk and therefore the buffer must eventually be written back to disk.) |
| BH_Lock | Buffer is undergoing disk I/O and is locked to prevent concurrent access. |
| BH_Req | Buffer is involved in an I/O request. |
| BH_Mapped | Buffer is a valid buffer mapped to an on-disk block. |
| BH_New | Buffer is newly mapped via `get_block()` and not yet accessed. |
| BH_Async_Read | Buffer is undergoing asynchronous read I/O via `end_buffer_async_read()`. |
| BH_Async_Write | Buffer is undergoing asynchronous write I/O via `end_buffer_async_write()`. |
| BH_Delay | Buffer does not yet have an associated on-disk block (delayed allocation). |
| BH_Boundary | Buffer forms the boundary of contiguous blocks—the next block is discontinuous. |
| BH_Write_EIO | Buffer incurred an I/O error on write. |
| BH_Ordered | Ordered write. |
| BH_Eopnotsupp | Buffer incurred a "not supported" error. |
| BH_Unwritten | Space for the buffer has been allocated on disk but the actual data has not yet been written out. |
| BH_Quiet | Suppress errors for this buffer. |

The `bh_state_bits` enumeration also contains as the last value in the list a `BH_PrivateStart` flag. This is not a valid state flag but instead corresponds to the first usable bit of which other code can make use. All bit values equal to and greater than `BH_PrivateStart` are not used by the block I/O layer proper, so these bits are safe to use by individual drivers who want to store information in the b_state field. Drivers can base the bit values of their internal flags off this flag and rest assured that they are not encroaching on an official bit used by the block I/O layer.

The b_count field is the buffer's usage count. The value is incremented and decremented by two inline functions, both of which are defined in <linux/buffer_head.h>:

```c
static inline void get_bh(struct buffer_head *bh) {
	atomic_inc(&bh->b_count);
}

static inline void put_bh(struct buffer_head *bh) {
	atomic_dec(&bh->b_count);
}
```

Before manipulating a buffer head, you must increment its reference count via get_bh() to ensure that the buffer head is not deallocated out from under you. When finished with the buffer head, decrement the reference count via put_bh().

The physical block on disk to which a given buffer corresponds is the b_blocknr—the logical block on the block device described by b_bdev.

The physical page in memory to which a given buffer corresponds is the page pointed to by b_page. More specifically, b_data is a pointer directly to the block (that exists somewhere in b_page), which is b_size bytes in length. Therefore, the block is located in memory starting at address b_data and ending at address (b_data + b_size).

The purpose of a buffer head is to describe this mapping between the on-disk block and the physical in-memory buffer (which is a sequence of bytes on a specific page). Acting as a descriptor of this buffer-to-block mapping is the data structure's only role in the kernel.

Before the 2.6 kernel, the buffer head was a much more important data structure: It was the unit of I/O in the kernel. Not only did the buffer head describe the disk-block-to-physical-page mapping, but it also acted as the container used for all block I/O. This had two primary problems. First, the buffer head was a large and unwieldy data structure (it has shrunken a bit nowadays), and it was neither clean nor simple to manipulate data in terms of buffer heads. Instead, the kernel prefers to work in terms of pages, which are simple and enable for greater performance. A large buffer head describing each individual buffer (which might be smaller than a page) was inefficient. Consequently, in the 2.6 kernel, much work has gone into making the kernel work directly with pages and address spaces instead of buffers. Some of this work is discussed in Chapter 16, “The Page Cache and Page Writeback,” where the address_space structure and the pdflush daemons are discussed.

The second issue with buffer heads is that they describe only a single buffer. When used as the container for all I/O operations, the buffer head forces the kernel to break up potentially large block I/O operations (say, a write) into multiple buffer_head structures.
