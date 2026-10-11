+   ▪ **Inode Table.** File information is stored in this table that includes owners, access permissions, time stamps, and links to the data blocks in which the data is located.

+   ▪ **Data Blocks.** This is where the actual data is located.

The ext2 file system format can process filenames with a length of up to 255 characters. With the path, a name can be a maximum of 4096 characters in length (slashes included).

A file can be up to 16 GB in size for a block size of 1024 bytes or two TB for a block size of 4096 bytes. The maximum file system size is two TB (with a block size of 1024 bytes) or 16 TB (with a block size of 4096 bytes).

![](bbox=[0.24, 0.43, 0.29, 0.48])

> The limitation on file size remains for the ext2 file system. However, the kernel can now handle files of almost any size.

# ReiserFS Format

On a file system with ext2 and a block size of 1024 bytes, a file 8195 bytes in size occupies 8 blocks completely and a ninth block with three bytes.

Even though only three bytes are occupied, the block is no longer available. This means that approximately 11 percent of available space is wasted.

If the file is 1025 bytes in size, two blocks are required, one of which is almost completely empty. Almost 50 percent of the space is wasted.

A worst case occurs if the file is very small: even if the file is only 50 bytes in size, a whole block is used (95 percent wasted).