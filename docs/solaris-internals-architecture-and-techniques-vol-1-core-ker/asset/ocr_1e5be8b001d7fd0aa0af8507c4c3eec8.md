# Anonymous Memory

# 5.5 Anonymous Memory

At many points we have mentioned anonymous memory. Anonymous memory refers to pages that are not directly associated with a vnode. Such pages are used for a process's heap space, its stack, and copy-on-write pages. In the Solaris kernel, two subsystems are dedicated to managing anonymous memory: the anon layer and the swaps file system.

The anonymous memory allocated to the heap of a process is a result of zero-fill-on-demand operation (ZFOD). The ZFOD operation is how we allocate new pages. A ZFOD occurs when we touch a memory address for the first time, and a new page of memory is dynamically allocated at that address. ZFOD is the allocation method used for heap space and /dev/zero with segment protection of MAP_FAULT. A page fault on a segment of this type will be recognized as ZFOD, and a new zeroed anonymous memory page is created at the fault location. The seg_vn segment fault handler, segvn_fault, handles the fault and creates ZFOD pages.

The seg_vn driver allocates anonymous memory to the segment by calling into the anonymous memory layer interfaces and attaching anonymous maps to the amp (anonymous map pointer) in the segvn_data structure. Figure 5.12 shows the seg_vn segment with the anonymous map structures allocated to it.

Every allocated page-sized piece of virtual memory in the segment is assigned an anonymous map. For example, when a segment is created, there are no anonymous map slots, but the first time a zero-fill-on-demand page fault occurs, a slot is allocated for a page, corresponding to the address within the segment where the fault occurred. At that time, a physical page is attached to the slot, the page may be stolen and no page is associated with, but an empty slot remains.

# 5.5.1 The Anonymous Memory Layer

Anonymous pages are created through the anon layer interfaces. The first time a segment receives a page fault, it allocates an anon map structure (which describes where to find the anon header) and puts a pointer to the anon header into the amp field of the anonymous map. It then allocates the slot array, big enough to hold the number of potential pages in the segment. The slot array is either a single or double indirection list, depending on how many slots are required.

32-bit systems require double indirection for segments larger than 16 Mbytes; 64-bit systems, because of larger pointer sizes, require double indirection for segments larger than 8 Mbytes. When we use single indirection, the anon header array_chunk directly references the slot array. When we use double indirection, the array is broken into chunks: 2048 slot chunks for 32-bit systems and 102