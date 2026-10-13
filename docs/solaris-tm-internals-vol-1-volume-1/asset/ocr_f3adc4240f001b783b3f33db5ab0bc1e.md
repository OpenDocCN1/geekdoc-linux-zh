ory, etc.), so a lighter-weight driver (`seg_map`) performs the mapping. The read and write file system calls require only a few basic mapping functions since they do not map files into a process's address space. Instead, they copy data to or from the process during a system call to a portion of the file that is mapped into the kernel's address space by `seg_map`. The lighter-weight `seg_map` driver enhances performance by virtue of a shorter code path and reduced locking complexities.

# 13.4.3 The seg_map Segment

The `seg_map` segment maintains mappings of pieces of files into the kernel address space and is used only by the file systems. Every time a read or write system call occurs, the `seg_map` segment driver locates or creates a virtual address space where the page of the file can be mapped. Then, the system call can copy the data to or from the user address space.

The `seg_map` segment provides a full set of segment driver interfaces (see “Memory Segments” on page 143); however, the file system directly uses a small subset of these interfaces without going through the generic segment interface. The subset handles the bulk of the work that is done by the `seg_map` segment for file read and write operations. The functions used by the file systems are shown in Table 13-8.

**Table 13-8** *seg_map Functions Used by the File Systems*

| Function Name | Description |
|---|---|
| `segmap_getmap()` | Retrieves or creates a mapping for a range of the file at the given offset and length. |
| `segmap_getmapfault()` |  |
| `segmap_release()` | Releases the mapping for a given file at a given address. |
| `segmap_pagecreate()` | Creates new page(s) of memory and slots in the `seg_map` segment for a given file. Used for extending files or writing to holes during a write. |
| `segmap_pageunlock()` | Unlocks pages in the segment that was locked during `segmap_pagecreate()`. |

At any time, the `seg_map` segment has some portion of the total file system cache mapped into the kernel address space. The maximum size of the `seg_map` segment differs among hardware architectures, is often only a fraction of the total physical memory size, and contains only a small proportion of the total file system cache. Note that even though the size of the `seg_map` segment is fixed, the pages which it references can be stolen by the page scanner, and as a result, only a portion of the `seg_map` segment may be resident (especially on machines where the `seg_map` segment is close to the size of physical memory).

A single `seg_map` segment is created at boot time. The segment is sized according to a table of machine types (see Table 13-9) and is capped at the amount of free