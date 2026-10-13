the file’s blocks (through the block map functions discussed in “Mapping of Files to Disk Blocks” on page 592) and reads them by calling the underlying device’s strategy routine.

Once the page is read by the file system, the requested range is copied back to the user by the `uio_move()` function. Then, the file system releases the slot associated with that block of the file with the `segmap_release()` function. At this point, the slot is not removed from the segment because we may need the same file and offset later (effectively caching the virtual address mapping); instead, it is added onto a `seg_map` free list so it can be reclaimed or reused later.

# 14.3.2.2 ufs_write()

Writing to the file system is performed in a similar manner, although it is more complex because of some of the file system write performance enhancements, such as delayed writes and write clustering. Writing to the file system follows the steps shown in Figure 14.8.

The write system call calls the file-system-independent write, which in our example calls `ufs_write()`. UFS breaks the write into 8-KByte chunks and then processes each chunk. For each 8-KByte chunk, the following steps are performed.

+   - UFS asks the segmap driver for an 8-KByte mapping of the file in the kernel’s virtual address space. The page for the file and offset is mapped here so that the data can be copied in and then written out with pages I/O.
+   - The segmap segment looks in its cache of mappings. If a mapping exists, it is returned. If there is no mapping for this file and offset, then a new one is created by replacement of one of the existing mappings.
+   - If the write is to a whole file system block, then a new zeroed page is created with `segmap_pagecreate()`. In the case of a partial block write, the block must first be read in so the partial block contents can be replaced.
+   - The new page is returned, locked, to UFS. The buffer that is passed into the write system call is copied from user address space into kernel address space.
+   - The `ufs_write` throttle first checks to see if too many bytes are outstanding for this file as a result of previous delayed writes. If more than the kernel parameter `ufs_HW` bytes are outstanding, the write is put to sleep until the amount of outstanding bytes drops below the kernel parameter `ufs_LW`.
+   - The file system calls the `seg_map` driver to map in the portion of the file we are going to write. The data is copied from the process’s user address space into the kernel address space allocated by `seg_map`, then `seg_map` is called to release the address space containing the dirty pages to be written. This is when the real work of write starts, because `seg_map` calls `ufs_putpage()` when it releases and there are dirty pages in the address space it is releasing.