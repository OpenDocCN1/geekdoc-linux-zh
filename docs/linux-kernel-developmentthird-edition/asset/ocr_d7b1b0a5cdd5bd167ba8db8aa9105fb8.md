The **flags** parameter specifies flags that correspond to the remaining VMA flags. These flags specify the type and change the behavior of the mapping. They are also defined in `+asm/mmman.h+`. See Table 15.3.

# Table 15.3    Map Type Flags

| Flag | Effect on the New Interval |
| --- | --- |
| MAP_SHARED | The mapping can be shared. |
| MAP_PRIVATE | The mapping cannot be shared. |
| MAP_FIXED | The new interval *must* start at the given address `addr` . |
| MAP_ANONYMOUS | The mapping is not file-backed, but is anonymous. |
| MAP_GROWSDOWN | Corresponds to `VM_GROWSDOWN` . |
| MAP_DENYWRITE | Corresponds to `VM_DENYWRITE` . |
| MAP_EXECUTABLE | Corresponds to `VM_EXECUTABLE` . |
| MAP_LOCKED | Corresponds to `VM_LOCKED` . |
| MAP_NORESERVE | No need to reserve space for the mapping. |
| MAP_POPULATE | Populate (prefault) page tables. |
| MAP_NONBLOCK | Do not block on I/O. |


If any of the parameters are invalid, `do_mmap()` returns a negative value. Otherwise, a suitable interval in virtual memory is located. If possible, the interval is merged with an adjacent memory area. Otherwise, a new `vm_area_struct` structure is allocated from the `vm_area_cache` slab cache, and the new memory area is added to the address space's linked list and red-black tree of memory areas via the `vma_link()` function. Next, the `total_vm` field in the memory descriptor is updated. Finally, the function returns the initial address of the newly created address interval.

The `do_mmap()` functionality is exported to user-space via the `mmap()` system call. The `mmap()` system call is defined as

```
void    * mmap2(void *start, size_t length, int prot, int flags, int fd, off_t pgoff)
```

This system call is named `mmap2()` because it is the second variant of `mmap()`. The original `mmap()` took an offset in bytes as the last parameter; the current `mmap2()` receives the offset in pages. This enables larger files with larger offsets to be mapped. The original