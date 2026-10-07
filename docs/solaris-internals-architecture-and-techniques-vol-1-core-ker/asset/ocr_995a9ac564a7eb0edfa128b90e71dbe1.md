# Memory Segments

segment driver constructor as an argument, which in turn calls into the seg_vn segment driver to create the mapping. The segment object is created and inserted into the segment list for the address space (struct as), and from that point on, the address space can perform operations on the mapping without knowing what the underlying segment is.

The address space segment routines can operate on the segment without knowing what type of segment is by calling the segment operation macros. For example, if the address space wants to call the fault handler for a segment, it calls SEGOP_FAULT(), which invokes the segment-specific page fault method, as shown below.

```
#define SEGOP_FAULT(h, s, a, l, t, rw) \
(*s)->s_cps->fault(h), (s), (a), (l), (t), (rw))
```

# Header File <vm/seg.h>

The Solaris kernel is implemented with a range of segment drivers for various functions. The different types of drivers are shown in Table 5-3. Most of the process address space mapping—including executable text, data, heap, stack and memory mapped files—is performed with the vnode segment driver, seg_vn. Other types of mappings that don't have vnodes associated with them require different segment drivers. The other segment drivers are typically associated with kernel memory mappings or hardware devices, such as graphics adapters.

# Table 5-3 Solaris 7 Segment Drivers

| Segment | Function |
| seg_vn | The vnode mappings into process address spaces are managed with the seg_vn device driver. Executable text and data, shared libraries, mapped files, heap and stack (heap and stack are anonymous) are all mapped with seg_vn. |
| seg_kmem | The segment from the bulk of nonpageable kernel memory is allocated. (See Chapter 6, "Kernel Memory") |
| seg_kp | The segment from which pageable kernel memory is allocated. Only a very small amount of the kernel is pageable; kernel threads and TNFF buffers are the main consumers of pageable kernel memory. |
| seg_spt | Shared page segment driver. Fast System V shared memory is mapped into process address space from this segment driver. Memory allocated from this driver is also known as Intimate Shared Memory (ISM). |
| seg_map | The kernel uses the seg_map driver to map files (vnodes) into the kernel's address space, to implement file system caching |
| seg_dev | Mapped hardware devices. |