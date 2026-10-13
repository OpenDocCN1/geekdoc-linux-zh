The segkmem segment driver implements the segment driver methods described in Section 5.4, “Memory Segments,” on page 143, to create general-purpose, non-pageable memory segments in the kernel address space. The segment driver does little more than implement the segkmem_create method to simply link segments into the kernel’s address space. It also implements protection manipulation methods, which load the correct protection modes via the HAT layer for segkmem segments. The set of methods implemented by the segkmem driver is shown in Table 6-5.

# Table 6-5 *Solaris 7 segkmem Segment Driver Methods*

| Function | Description |
|---|---|
| `segkmem_create()` | Creates a new kernel memory segment. |
| `segkmem_setprot()` | Sets the protection mode for the supplied segment. |
| `segkmem_checkprot()` | Checks the protection mode for the supplied segment. |
| `segkmem_getprot()` | Gets the protection mode for the current segment. |

The second function of the segkmem driver is to implement a page-level memory allocator by combined use of the resource map allocator and page allocator. The page-level memory allocator within the segkmem driver is implemented with the function kmem_getpages(). The kmem_getpages() function is the kernel’s central allocator for wired-down, page-sized memory requests. Its main client is the second-level memory allocator, the slab allocator, which uses large memory areas allocated from the page-level allocator to allocate arbitrarily sized memory objects. We’ll cover more on the slab allocator further in this chapter.

The kmem_getpages() function allocates page-sized chunks of virtual address space from the kernelmap segment. The kernelmap segment is only one of many segments created by the segkmem driver, but it is the only one from which the segkmem driver allocates memory.

The resource map allocator allocates portions of virtual address space within the kernelmap segment but on its own does not allocate any physical memory resources. It is used together with the page allocator, page_create_va(), and the hat_memload() functions to allocate physical mapped memory. The resource map allocator allocates some virtual address space, the page allocator allocates pages, and the hat_memload() function maps those pages into the virtual address space provided by the resource map. A client of the segkmem memory allocator can acquire pages with kmem_getpages() and then return them to the map with kmem_freepages, as shown in Table 6-6.

Pages allocated through kmem_getpages are not pageable and are one of the few exceptions in the Solaris environment where a mapped page has no logically associated vnode. To accommodate that case, a special vnode, kvp, is used. All pages created through the segkmem segment have kvp as the vnode in their identity—this allows the kernel to identify wired-down kernel pages.