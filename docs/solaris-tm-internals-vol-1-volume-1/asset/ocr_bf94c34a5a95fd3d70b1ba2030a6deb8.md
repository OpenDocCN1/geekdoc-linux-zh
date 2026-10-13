address and length of the mapping, then creates a seg_vn-specific data structure within the segment structure's s_data field. The seg_vn-specific data structure holds all of the information the seg_vn driver needs to handle the address mappings for the segment.

The seg_vn-specific data structure (struct segvn_data) contains pointers to the vnode that is mapped to and any anonymous memory that has been allocated for this segment. The file system does most of the work of mapped files once the mapping is created. As a result, the seg_vn driver is fairly simple—most of the seg_vn work is done during creation and deletion of the mapping.

The more complex part of the seg_vn driver implementation is its handling of anonymous memory pages within the segment, which we discuss in the sections that follow. When we create a file mapping, we put the vnode and offset of the file being mapped into the segvn_data structure members, vp and offset. The seg_vn data structure is shown below; Figure 5.10 illustrates the seg_vn segment driver vnode relationship.

```
```c
struct segvn_data {
    krwlock_t lock;          /* protect segvn_data and vpage array */
    uchar_t pagprot;         /* true if per page protections present */
    uchar_t prot;            /* current segment prot if pageprot == 0 */
    uchar_t maxprot;         /* maximum segment protections */
    uchar_t type;            /* type of sharing done */
    u_offset_t offset;       /* starting offset of vnode for mapping */
    struct vnode *vp;        /* vnode that segment mapping is to */
    ulong_t anon_index;      /* starting index into anon_map anon array */
    struct anon_map *amp;    /* pointer to anon share structure, if needed */
    struct vpage *vpage;     /* per-page information, if needed */
    struct cred *cred;       /* mapping credentials */
    size_t swresv;           /* swap space reserved for this segment */
    uchar_t advice;          /* madvise flags for segment */
    uchar_t pageadvice;      /* true if per page advise set */
    struct flags;            /* flags from psm/anon_map */
    usize_t softlockcnt;     /* # of pages SOFTLOCKED in seg */
};
```
```

# Header File  `<vm/seg_vn.h>`

Creating a mapping for a file is done with the mmap() system call, which calls the map method for the file system that contains the file. For example, calling mmap() for a file on a UFS file system will call ufs_map(), which in turn calls into the seg_vn driver to create a mapped file segment in the address space with the segvn_create() function.

At this point we create an actual virtual memory mapping by talking to the hardware through the hardware address translation functions by using the hat_map() function. The hat_map() function is the central function for creating address space mappings. It calls into the hardware-specific memory implementation for the platform to program the hardware MMU, so that memory address references within the supplied address range will trigger the page fault handler in the segment driver until a valid physical memory page has been placed at the