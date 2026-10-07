# 5.4.2 Copy-on-Write

The copy-on-write process occurs when a process writes to a page that is mapped with MAP PRIVATE. This process prevents other mappings to the page from seeing changes that are made. seg_vn implements a copy-on-write by setting the hardware-MMU permissions of a segment to read-only and setting the segment permissions to read-write. When a process attempts to write to a mapping that is configured this way, the MMU generates an exception and causes a page fault on the page. The page fault handler in seg_vn looks at the protection mode for the segment; if it is mapped private and read-write, the handler initiates a copy-on-write.

The copy-on-write unmaps the shared vnode page where the fault occurred, creates a page of anonymous memory at that address, and then copies the contents of the old page to the new anonymous page. All of this happens in the context of the page fault, so the process never knows what's happening underneath.

The copy-on-write operation behaves slightly differently under different conditions. When memory is low, rather than creating a new physical memory page, the copy-on-write steals the page from the offset of the file underneath and renames it to the new anonymous page. This only occurs when free memory is lower than the system parameter minfree.

# 5.4.3 Page Protection and Advice

The seg_vn supports memory protection modes on either the whole segment or individual pages within a segment. Whole segment protection is implemented by the seg_vn data structure member, prot; its enablement depends on the boolean switch, pageprot, in the seg_vn data structure. If pageprot is equal to zero, the entire segment's protection mode is set by prot; otherwise, page-level protection is enabled.

Page-level protection is implemented by an array of page descriptors pointed by the vpage structure, shown below. If page-level protection is enabled, the vpage points to an array of vpage structures. Every possible page in the address space has one array entry, which means that the number of vpage members is the virtual address space size divided by the fundamental page size (8 Kbytes by UltraSPARC).

```
struct vpage {
    uchar_t nvn_prot;      /* see <sys/mman.h> prot flags */
    uchar_t nvn_advice;     /* pplock <sys/mman.h> madvise flags */
};
```

Header File <vm/vpage.h>

The ventry for each page uses the standard memory protection bits from Table 5-5. The per-page vpage structures are also used to implement memory advice for mapped files in the seg_vn segment. (See “Providing Advice to the Memory System” on page 502.).