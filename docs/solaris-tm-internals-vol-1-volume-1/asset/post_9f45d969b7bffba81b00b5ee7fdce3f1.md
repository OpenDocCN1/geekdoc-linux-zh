
memory, etc.), so a lighter-weight driver (`seg_map`) performs the mapping. The read and write file system calls require only a few basic mapping functions since they do not map files into a process's address space. Instead, they copy data to or from the process during a system call to a portion of the file that is mapped into the kernel's address space by `seg_map`. The lighter-weight `seg_map` driver enhances performance by virtue of a shorter code path and reduced locking complexities.

## 13.4.3 The seg_map Segment

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

A single `seg_map` segment is created at boot time. The segment is sized according to a table of machine types (see Table 13-9) and is capped at the amount of free memory just after the kernel has booted. For example, if the machine is an Ultra-1 or sun4u architecture, the maximum size of the seg_map is 256 Mbytes. A 64-Mbyte machine booting the Solaris kernel will most likely end up with a seg_map segment about 50 Mbytes in size, as 50 Mbytes was the free memory when the system was being booted. A 512-Mbyte sun4u system will have a seg_map size of 256 Mbytes, since free memory will be much larger than 256 Mbytes while it is booting.

**Table 13-9** *Architecture-Specific Sizes of Solaris 7* `seg_map` *Segment*

| Architecture | Systems | Maximum Size of `seg_map` |
|---|---|---|
| sun4c | SPARC 1, 2 | 4 Mbytes |
| sun4m | SPARC 5, 10, 20 | 16 Mbytes |
| sun4d | SPARC 1000,2000 | 32 Mbytes |
| sun4u | UltraSPARC | 256 Mbytes |

We can take a look at the `seg_map` segment on a running system by using adb with the $seg macro, as shown below.

```text
# adb -k /dev/ksyms /dev/mem
physmem 3b73

segmap/
segmap:
segmap:             3000022df50

3000022df50$<seg

3000022df50:       base             size             as
                   2a75000000       7432000          104236e0
3000022df68:       next             prev             op
                   104234a0         3000022df88      segmap_ops
3000022df80:       data
                   300001b1d68
```

We can see that on this system, the segmap segment has been created at boot as 0x7432000 bytes, or 121,839,616 bytes. This system was a 128-Mbyte Ultra-1, and we can see that free memory was smaller than the 256-Mbyte maximum segment size for the sun4u architecture. Hence, the segment was created at whatever the size of free memory was at that point. Once segmap is created, the segment interfaces are called directly from the file system code during the read and write operations.

The `seg_map` segment driver divides the segment into block-sized slots that represent blocks in the files it maps. The `seg_map` block size for the Solaris kernel is 8,192 bytes. A 128-Mbyte segmap segment would, for example, be divided into 128-MB/8-KB slots, or 16,384 slots. The seg_map segment driver maintains a hash list of its page mappings so that it can easily locate existing blocks. The list is based on file and offset. One list entry exists for each slot in the segmap segment.

The structure for each slot in a `seg_map` segment is defined in the `<vm/segmap.h>` header file, shown below.

```c
/*
 * Each smap struct represents a MAXBSIZE-sized mapping to the
 * <sm_vp, sm_off> given in the structure. The location of
 * the structure in the array gives the virtual address of the
 * mapping. Structure rearranged for 64-bit sm_off.
 */
struct smap {
        struct vnode   *sm_vp;       /* vnode pointer (if mapped) */

        /*
         * These next 3 entries are coded as
         * ushort_t's if we wish to cache or remove.
         */
        struct smap    *sm_hash;     /* hash pointer */
        struct smap    *sm_next;     /* next pointer */
        struct smap    *sm_prev;     /* previous pointer */
        u_offset_t     sm_off;       /* file offset for mapping */

        ushort_t       sm_bitmap;    /* bitmap for locked translations */
        ushort_t       sm_refcnt;    /* reference count for uses */
};

struct smfree {
        struct smap    *sm_free;     /* free list array pointer */
                struct smap *sm_mtx; /* protects smap data of this color */
        kcondvar_t     sm_free_cv;
        ushort_t       sm_want;      /* someone wants a slot of this color */
};
```

**Header File** `<vm/seg_map.h>`

The smap structures are:

- **sm_vp** — The file (vnode) this slot represents (if slot not empty)
- **sm_hash, sm_next, sm_prev** — Hash list reference pointers
- **sm_off** — The file (vnode) offset for a block-sized chunk in this slot in the file
- **sm_bitmap** — Bitmap to maintain translation locking
- **sm_refcnt** — The number of references to this mapping caused by concurrent reads

The important fields in the smap structure are the file and offset fields, `sm_vp` and `sm_off`. These fields identify which page of a file is represented by each slot in the segment.

We can observe the `seg_map` slot activity with the `kstat` statistics that are collected for the `seg_map` segment driver. These statistics are visible with the `netstat` command, as shown below.

```text
# netstat -k segmap
segmap:
fault 8366623 faulta 0 getmap 16109564 get_use 11723 get_reclaim 15257790 get_reuse 825178
get_unused 0 get_nofree 0 rel_async 710244 rel_write 749677 rel_free 16370
rel_abort 0 rel_dontneed 709733 release 15343517 prefetch 1009281
```

**Table 13-10** *Statistics from the `seg_map` Segment Driver*

| Field Name | Description |
|---|---|
| `fault` | The number of times `segmap_fault` was called, usually as a result of a read or write system call. |
| `faulta` | The number of times the `segmap_faulta` function was called. It is called to initiate asynchronous paged I/O on a file. |
| `getmap` | The number of times the `segmap_getmap` function was called. It is called by the read and write system calls each time a read or write call is started. It sets up a slot in the `seg_map` segment for the requested range on the file. |
| `get_use` | The number of times getmap found an empty slot in the segment and used it. |
| `get_reclaim` | The number of times getmap found a valid mapping for the file and offset already in the `seg_map` segment. |
| `get_reuse` | The number of times getmap deleted the mapping in a nonempty slot and created a new mapping for the file and offset requested. |
| `get_unused` | Not used—always zero. |
| `get_nofree` | The number of times a request for a slot was made and none was available on the internal free list of slots. This number is usually zero because each slot is put on the free list when release is called at the end of each I/O. Hence, ample free slots are usually available. |
| `rel_async` | The slot was released with a delayed I/O on it. |
| `rel_write` | The slot was released as a result of a write system call. |
| `rel_free` | The slot was released, and the VM system was told that the page may be needed again but to free it and retain its file/offset information. These pages are placed on the cache list tail so that they are not the first to be reused. |
