
routine of the segment driver for this segment (in this case, the vnode segment driver).

- 4. The segment driver allocates and maps a page of memory by calling into the HAT layer and then copies the contents of the page from the swap device.
- 5. The segment driver reads the page from the backing store by calling the `getpage()` function of the backing store’s vnode.
- 6. The backing store for this segment is the swap device, so the swap device `getpage()` function is called to read in the page from the swap device.

Once this process is completed, the process can continue execution.

## 5.4 Memory Segments

Another example of the object-oriented approach to memory management is the memory “segment” object. Memory segments manage the mapping of a linear range of virtual memory into an address space. The mapping is between the address space and some type of device. The objective of the memory segment is to allow both memory and devices to be mapped into an address space. Traditionally, this required hard-coding memory and device information into the address space handlers for each device. The object architecture allows different behaviors for different segments.

For example, one segment might be a mapping of a file into an address space (with `mmap`), and another segment might be the mapping of a hardware device into the process’s address space (a graphics framebuffer). In this case, the segment driver provides a similar view of a linear address space, even though the file mapping operation with `mmap` uses pages of memory to cache the file data, whereas the framebuffer device maps the hardware device into the address space.

The flexibility of the segment object allows us to use virtually any abstraction to represent a linear address space that is visible to a process, regardless of the real facilities behind the scenes.

```c
struct seg {
        caddr_t s_base;             /* base virtual address */
        size_t  s_size;             /* size in bytes */
        struct as *s_as;            /* containing address space */
        seg_next s_next;            /* next seg in this address space */
        struct seg *s_prev;         /* prev seg in this address space */
        struct seg_ops *s_ops;      /* ops vector: see below */
        void *s_data;               /* private data for instance */
};
```

**Header File** `<vm/seg.h>`

To implement an address space, a segment driver implementation is required to provide at least the following: functions to create a mapping for a linear address range, page fault handling routines to deal with machine exceptions within that linear address range, and a function to destroy the mapping. These functions are packaged together into a **segment driver**, which is an instantiation of the segment object interface. Figure 5.9 illustrates the relationship between an address space and a segment and shows a segment mapping the heap space of a process.

![](img/220ae4af07df2fe8e5be69d27f885d1b_185_0.png)

**Figure 5.9** *Segment Interface*

A segment driver implements a subset of the methods described in Table 5-4 on page 146, as well as a constructor function to create the first instance of the object. Functions in the segment operations structure, s_ops, point to functions within the vnode segment driver and are prefixed with segvn. A segment object is created when another subsystem wants to create a mapping by calling as_map() to create a mapping at a specific address. The segment's create routine is passed as an argument to as_map(), a segment object is created, and a segment object pointer is returned. Once the segment is created, other parts of the virtual memory system can call into the segment for different address space operations without knowing what the underlying segment driver is or what the segment method operations are.

For example, when a file is mapped into an address space with mmap(), the address space map routine as_map() is called with segvn_create() (the vnode segment driver constructor) as an argument, which in turn calls into the seg_vn segment driver to create the mapping. The segment object is created and inserted into the segment list for the address space (struct as), and from that point on, the address space can perform operations on the mapping without knowing what the underlying segment is.

The address space routines can operate on the segment without knowing what type of segment is underlying by calling to the segment operation macros. For example, if the address space layer wants to call the fault handler for a segment, it calls `SEGOP_FAULT()`, which invokes the segment-specific page fault method, as shown below.

```c
#define SEGOP_FAULT(h, s, a, l, t, rw) \
        (*(s)->s_ops->fault)((h), (s), (a), (l), (t), (rw))
```

**Header File** `<vm/seg.h>`

The Solaris kernel is implemented with a range of segment drivers for various functions. The different types of drivers are shown in Table 5-3. Most of the process address space mapping—including executable text, data, heap, stack and memory mapped files—is performed with the vnode segment driver, seg_vn. Other types of mappings that don’t have vnodes associated with them require different segment drivers. The other segment drivers are typically associated with kernel memory mappings or hardware devices, such as graphics adapters.

### Table 5-3 Solaris 7 Segment Drivers

| Segment | Function |
|---|---|
| `seg_vn` | The vnode mappings into process address spaces are managed with the seg_vn device driver. Executable text and data, shared libraries, mapped files, heap and stack (heap and stack are anonymous memory) are all mapped with seg_vn. |
| `seg_kmem` | The segment from which the bulk of nonpageable kernel memory is allocated. (See Chapter 6, “Kernel Memory”). |
| `seg_kp` | The segment from which pageable kernel memory is allocated. Only a very small amount of the kernel is pageable; kernel thread stacks and TNF buffers are the main consumers of pageable kernel memory. |
| `seg_spt` | Shared page table segment driver. Fast System V shared memory is mapped into process address space from this segment driver. Memory allocated from this driver is also known as Intimate Shared Memory (ISM). |
| `seg_map` | The kernel uses the seg_map driver to map files (vnodes) into the kernel’s address space, to implement file system caching. |
| `seg_dev` | Mapped hardware devices. |
| `seg_mapdev` | Mapping support for mapped hardware devices, through the `ddi_mapdev(9F)` interface. |
| `seg_lock` | Mapping support for hardware graphics devices that are mapped between user and kernel address space. |
| `seg_drv` | Mapping support for mapped hardware graphics devices. |
| `seg_nf` | Nonfaulting kernel memory driver. |
| `seg_mdi` | Hardware mapping support for the cgfourteen graphics framebuffer. |
| `seg_sx` | Hardware mapping support for the SPARCstation 20 SX graphics framebuffer. |

### Table 5-4 Solaris 7 Segment Driver Methods

Table 5-4 describes segment driver methods implemented in Solaris 7.

| Method | Description |
|---|---|
| `advise()` | Provides a hint to optimize memory accesses to this segment. For example, sequential advice given to mapped files causes read-ahead to occur. |
| `checkprot()` | Checks that the requested access type (read, write, exec) is allowed within the protection level of the pages within the segment. |
| `dump()` | Dumps the segment to the dump device; used for crash dumps. |
| `dup()` | Duplicates the current memory segment, including all of the page mapping entries to the new segment pointer provided. |
| `fault()` | Handles a page fault for a segment. The arguments describe the segment, the virtual address of the page fault, and the type of fault. |
| `faulta()` | Starts a page fault on a segment and address asynchronously. Used for read-ahead or prefetching of data as a performance optimization for I/O. |
| `free()` | Destroys a segment. |
| `getmemid()` | Gets a unique identifier for the memory segment. |
| `getoffset()` | Queries the segment driver for the offset into the underlying device for the mapping. (Not meaningful on all segment drivers.) |
| `getprot()` | Asks the segment driver for the protection levels for the memory range. |
| `gettype()` | Queries the driver for the sharing modes of the mapping. |
