```
```assembly
		"movl $0, %&cr3;\t\n" \
		: "=r" (tmpreg) \
		: : "memory");
	} while (0)
```
```

# ## Page Allocation and Deallocation

The page allocator in kernel 2.4 is zone based. The physical memory is split into zones. The allocator tries to coalesce free memory in big chunks of physical contiguous memory. The chunks are naturally aligned in the physical memory. Order is 0 for allocating or freeing a single page. Order is 1 for allocating two contiguous physical pages (for example the task struct + kernel stack is allocated with order 1, because it’s 8,192 bytes in size). For hashtables, the order grows much more—up to allocating 2Mbytes of contiguous physical memory.

The mechanisms and data structures used for page allocation and deallocation are perhaps the most critical in maintaining the efficiency of the virtual memory subsystem. All the physical pages in the system are described by the mem_map data structure, which is a linked list of mem_map_t . Each mem_map_t describes a single physical page in the system. Important fields (so far as memory management is concerned) are:

+   * count—This is a count of the number of users of this page. The count is greater than one when the page is shared between many processes.
+   * age—This field describes the age of the page and is used to decide if the page is a good candidate for discarding or swapping.
+   * map_nr—This is the physical PFN that the mem_map_t describes.

The free_area structure is used by the page allocation code to find and free pages. The whole buffer management scheme is supported by this mechanism and, so far as the code is concerned, the size of the page and physical paging mechanisms used by the CPU are irrelevant.

Each element of free_area contains information about blocks of pages. The first element in the array describes single pages, the next, blocks of two pages, and so on upwards in powers of two. The list element is used as a queue head and has pointers to the page structures in the mem_map array. Free blocks of pages are queued here. map is a pointer to a bitmap, which keeps track of allocated groups of pages of this size. Bit N of the bitmap is set if the Nth block of pages is free.