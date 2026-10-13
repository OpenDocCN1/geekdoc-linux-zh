
free and which parts are allocated, so that we know where to satisfy new requests. To record the information, we use a general-purpose allocator to keep track of the start and length of the mappings that are allocated from the kernel map area. The allocator we use is the resource map allocator, which is used almost exclusively for managing the kernel virtual address space.

The kernel map area is large, up to 8 Gbytes on 64-bit sun4u systems, and can quickly become fragmented if it accommodates many consumers with different-sized requests. It is up to the resource map allocator to try to keep the kernel map area as unfragmented as possible.

### 6.2.2 The Resource Map Allocator

Solaris uses the resource map allocator to manage the kernel map. To keep track of the areas of free memory within the map, the resource map allocator uses a simple algorithm to keep a list of start/length pairs that point to each area of free memory within the map. The map entries are sorted in ascending order to make it quicker to find entries, allowing faster allocation. The map entries are shown in the following map structure, which can be found in the `<sys/map.h>` header file.

```
struct map {
        size_t  m_size;        /* size of this segment of the map */
        ulong_t m_addr;        /* resource-space addr of start of segment */
};
```

Header File  `<vm/rm.h>`

The area managed by the resource map allocator is initially described by just one map entry representing the whole area as one contiguous free chunk. As more allocations are made from the area, more map entries are used to describe the area, and as a result, the map becomes ever more fragmented over time.

The resource map allocator uses a first-fit algorithm to find space in the map to satisfy new requests, which means that it attempts to find the first available slot in the map that fits the request. The first-fit algorithm provides a fast find allocation at the expense of map fragmentation after time. For this reason, it is important to ensure that kernel subsystems do not perform an excessive amount of map allocation and freeing. The kernel slab allocator (discussed next) should be used for these types of requests.

Map resource requests are made with the rmalloc() call, and resources are returned to the map by rmfree(). Resource maps are created with the rmallocmap() function and destroyed with the rmfreemap() function. The functions that implement the resource map allocator are shown in Table 6-4.

Table 6-4  *Solaris 7 Resource Map Allocator Functions from `<sys/map.h>`*

| Function | Description |
|---|---|
| `rmallocmap()` | Dynamically allocates a map. Does not sleep.<br>Driver-defined basic locks, read/write locks, and sleep locks can be held across calls to this function.<br>DDI-/DKI-conforming drivers may only use map structures that have been allocated and initialized with `rmallocmap()`. |
| `rmallocmap_wait()` | Dynamically allocates a map. It does sleep.<br>DDI-/DKI-conforming drivers can only use map structures that have been allocated and initialized with `rmallocmap()` and `rmallocmap_wait()`. |
| `rmfreemap()` | Frees a dynamically allocated map. Does not sleep.<br>Driver-defined basic locks, read/write locks, and sleep locks can be held across calls to this function.<br>Before freeing the map, the caller must ensure that nothing is using space managed by the map and that nothing is waiting for space in the map. |
| `rmalloc()` | Allocates *size* units from the given map. Returns the base of the allocated space. In a map, the addresses are increasing and the list is terminated by a 0 size. Algorithm is first-fit. |
| `rmalloc_wait()` | Like `rmalloc`, but waits if necessary until space is available. |
| `rmalloc_locked()` | Like `rmalloc`, but called with lock on map held. |
| `rmfree()` | Frees the previously allocated space at *addr* of *size* units into the specified map.<br>Sorts *addr* into map and combines on one or both ends if possible. |
| `rmget()` | Allocates *size* units from the given map, starting at address *addr*. Returns *addr* if successful, 0 if not. This may cause the creation or destruction of a resource map segment.<br>This routine returns failure status if there is not enough room for a required additional map segment. |

### 6.2.3 The Kernel Memory Segment Driver

The segkmem segment driver performs two major functions: it manages the creation of general-purpose memory segments in the kernel address space, and it also provides functions that implement a page-level memory allocator by using one of those segments—the kernel map segment.

The segkmem segment driver implements the segment driver methods described in Section 5.4, “Memory Segments,” on page 143, to create general-purpose, non-pageable memory segments in the kernel address space. The segment driver does little more than implement the segkmem_create method to simply link segments into the kernel’s address space. It also implements protection manipulation methods, which load the correct protection modes via the HAT layer for segkmem segments. The set of methods implemented by the segkmem driver is shown in Table 6-5.

Table 6-5 *Solaris 7 segkmem Segment Driver Methods*

| Function | Description |
|---|---|
| `segkmem_create()` | Creates a new kernel memory segment. |
| `segkmem_setprot()` | Sets the protection mode for the supplied segment. |
| `segkmem_checkprot()` | Checks the protection mode for the supplied segment. |
| `segkmem_getprot()` | Gets the protection mode for the current segment. |

The second function of the segkmem driver is to implement a page-level memory allocator by combined use of the resource map allocator and page allocator. The page-level memory allocator within the segkmem driver is implemented with the function kmem_getpages(). The kmem_getpages() function is the kernel’s central allocator for wired-down, page-sized memory requests. Its main client is the second-level memory allocator, the slab allocator, which uses large memory areas allocated from the page-level allocator to allocate arbitrarily sized memory objects. We’ll cover more on the slab allocator further in this chapter.

The kmem_getpages() function allocates page-sized chunks of virtual address space from the kernelmap segment. The kernelmap segment is only one of many segments created by the segkmem driver, but it is the only one from which the segkmem driver allocates memory.

The resource map allocator allocates portions of virtual address space within the kernelmap segment but on its own does not allocate any physical memory resources. It is used together with the page allocator, page_create_va(), and the hat_memload() functions to allocate physical mapped memory. The resource map allocator allocates some virtual address space, the page allocator allocates pages, and the hat_memload() function maps those pages into the virtual address space provided by the resource map. A client of the segkmem memory allocator can acquire pages with kmem_getpages() and then return them to the map with kmem_freepages(), as shown in Table 6-6.

Pages allocated through kmem_getpages are not pageable and are one of the few exceptions in the Solaris environment where a mapped page has no logically associated vnode. To accommodate that case, a special vnode, kvp, is used. All pages created through the segkmem segment have kvp as the vnode in their identity—this allows the kernel to identify wired-down kernel pages.

Table 6-6  *Solaris 7 Kernel Page Level Memory Allocator*

| Function | Description |
|---|---|
| `kmem_getpages()` | Allocates *npages* pages worth of system virtual address space, and allocates wired-down page frames to back them.<br><br>If *flag* is `KM_NOSLEEP`, blocks until address space and page frames are available. |
| `kmem_freepages()` | Frees *npages* (MMU) pages allocated with `kmem_getpages()`. |

### 6.2.4 The Kernel Memory Slab Allocator

In this section, we introduce the general-purpose memory allocator, known as the slab allocator. We begin with a quick walk-through of the slab allocator features, then look at how the allocator implements object caching, and follow up with a more detailed discussion on the internal implementation.

#### 6.2.4.1 Slab Allocator Overview

Solaris provides a general-purpose memory allocator that provides arbitrarily sized memory allocations. We refer to this allocator as the slab allocator because it consumes large slabs of memory and then allocates smaller requests with portions of each slab. We use the slab allocator for memory requests that are:

- Smaller than a page size
- Not an even multiple of a page size
- Frequently going to be allocated and *freed*, so would otherwise fragment the kernel map

The slab allocator was introduced in Solaris 2.4, replacing the *buddy* allocator that was part of the original SVR4 Unix. The reasons for introducing the slab allocator were as follows:

- The SVR4 allocator was slow to satisfy allocation requests.
- Significant fragmentation problems arose with use of the SVR4 allocator.
- The allocator footprint was large, wasting a lot of memory.
- With no clean interfaces for memory allocation, code was duplicated in many places.

The slab allocator solves those problems and dramatically reduces overall system complexity. In fact, when the slab allocator was integrated into Solaris, it resulted in a net reduction of 3,000 lines of code because we could centralize a great deal of the memory allocation code and could remove a lot of the duplicated memory allocator functions from the clients of the memory allocator.
