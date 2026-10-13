free and which parts are allocated, so that we know where to satisfy new requests. To record the information, we use a general-purpose allocator to keep track of the start and length of the mappings that are allocated from the kernel map area. The allocator we use is the resource map allocator, which is used almost exclusively for managing the kernel virtual address space.

The kernel map area is large, up to 8 Gbytes on 64-bit sun4u systems, and can quickly become fragmented if it accommodates many consumers with different-sized requests. It is up to the resource map allocator to try to keep the kernel map area as unfragmented as possible.

# 6.2.2 The Resource Map Allocator

Solaris uses the resource map allocator to manage the kernel map. To keep track of the areas of free memory within the map, the resource map allocator uses a simple algorithm to keep a list of start/length pairs that point to each area of free memory within the map. The map entries are sorted in ascending order to make it quicker to find entries. Allowing faster allocation. The map entries are shown in the following map structure, which can be found in the <sys/map.h> header file.

```
struct map {
        size_t  m_size;        /* size of this segment of the map */
        ulong_t m_addr;        /* resource-space addr of start of segment */
};
```

Header File  <vm/rm.h>

The area managed by the resource map allocator is initially described by just one map entry representing the whole area as one contiguous free chunk. As more allocations are made from the area, more map entries are used to describe the area, and as a result, the map becomes ever more fragmented over time.

The resource map allocator uses a first-fit algorithm to find space in the map to satisfy new requests, which means that it attempts to find the first available slot in the map that fits the request. The first-fit algorithm provides a fast find allocation at the expense of map fragmentation after time. For this reason, it is important to ensure that kernel subsystems do not perform an excessive amount of map allocation and freeing. The kernel slab allocator (discussed next) should be used for these types of requests.

Map resource requests are made with the rmalloc() call, and resources are returned to the map by rmfree(). Resource maps are created with the rmallocmap() function and destroyed with the rmfreemap() function. The functions that implement the resource map allocator are shown in Table 6-4.

# 6.2.3 The Kernel Memory Segment Driver

The segment segment driver performs two major functions: it manages the creation of general-purpose memory segments in the kernel address space, and it also