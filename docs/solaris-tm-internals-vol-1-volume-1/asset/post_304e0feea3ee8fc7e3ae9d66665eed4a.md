
The allocator interfaces are shown in Table 6-8.

**Table 6-8** *Solaris 7 Slab Allocator Interfaces from* `<sys/kmem.h>`

| Function | Description |
|---|---|
| `kmem_cache_create()` | Creates a new slab cache with the supplied *name*, aligning objects on the boundary supplied with alignment. The constructor, destructor, and reclaim functions are optional and can be supplied as NULL. An argument can be provided to the constructor with *arg*. The back-end memory allocator can also be specified or supplied as NULL. If a NULL back-end allocator is supplied, then the default allocator, `kmem_getpages()`, is used. Flags can be supplied as `KMC_NOTOUCH`, `KMC_NODEBUG`, `KMC_NOMAGAZINE`, and `KMC_NOHASH`. |
| `kmem_cache_destroy()` | Destroys the cache referenced by *cp*. |
| `kmem_cache_alloc()` | Allocates one object from the cache referenced by *cp*. Flags can be supplied as either `KM_SLEEP` or `KM_NOSLEEP`. |
| `kmem_cache_free()` | Returns the buffer *buf* to the cache referenced by *cp*. |
| `kmem_cache_stat()` | Returns a named statistic about a particular cache that matches the string name. Finds a name by looking at the kstat slab cache names with `netstat -k`. |

Caches are created with the `kmem_cache_create()` function, which can optionally supply callbacks for construction, deletion, and cache reclaim notifications. The callback functions are described in Table 6-9.

**Table 6-9** *Slab Allocator Callback Interfaces from* `<sys/kmem.h>`

| Function | Description |
|---|---|
| `constructor()` | Initializes the object *buf*. The arguments *arg* and *flag* are those provided during `kmem_cache_create()`. |
| `destructor()` | Destroys the object *buf*. The argument *arg* is that provided during `kmem_cache_create()`. |
| `reclaim()` | Where possible, returns objects to the cache. The argument is that provided during `kmem_cache_create()`. |

## 6.2.4.3 General-Purpose Allocations

In addition to object-based memory allocation, the slab allocator provides backward-compatible, general-purpose memory allocation routines. These routines allocate arbitrary-length memory by providing a method to `malloc()`. The slab allocator maintains a list of various-sized slabs to accommodate `kmem_alloc()` requests and simply converts the `kmem_alloc()` request into a request for an object from the nearest-sized cache. The sizes of the caches used for `kmem_alloc()` are named `kmem_alloc_n`, where *n* is the size of the objects within the cache (see Section 6.2.4.9, “Slab Allocator Statistics,” on page 229). The functions are shown in Table 6-10.

**Table 6-10** *General-Purpose Memory Allocation*

| Function | Description |
|---|---|
| `kmem_alloc()` | Allocates *size* bytes of memory. Flags can be either `KM_SLEEP` or `KM_NOSLEEP`. |
| `kmem_zalloc()` | Allocates *size* bytes of zeroed memory. Flags can be either `KM_SLEEP` or `KM_NOSLEEP`. |
| `kmem_free()` | Returns to the allocator the buffer pointed to by *buf* and *size*. |

## 6.2.4.4 Slab Allocator Implementation

The slab allocator implements the allocation and management of objects to the front-end clients, using memory provided by the back-end allocator. In our introduction to the slab allocator, we discussed in some detail the virtual allocation units: the object and the slab. The slab allocator implements several internal layers to provide efficient allocation of objects from slabs. The extra internal layers reduce the amount of contention between allocation requests from multiple threads, which ultimately allows the allocator to provide good scalability on large SMP systems.

Figure 6.5 shows the internal layers of the slab allocator. The additional layers provide a cache of allocated objects for each CPU, so a thread can allocate an object from a local per-CPU object cache without having to hold a lock on the global slab cache. For example, if two threads both want to allocate an inode object from the inode cache, then the first thread’s allocation request would hold a lock on the inode cache and would block the second thread until the first thread has its object allocated. The per-CPU cache layers overcome this blocking with an object cache per CPU to try to avoid the contention between two concurrent requests. Each CPU has its own short-term cache of objects, which reduces the amount of time that each request needs to go down into the global slab cache.

![](img/220ae4af07df2fe8e5be69d27f885d1b_265_0.png)

**Figure 6.5** *Slab Allocator Internal Implementation*

The layers shown in Figure 6.5 are separated into the slab layer, the depot layer, and the CPU layer. The upper two layers (which together are known as the magazine layer) are caches of allocated groups of objects and use a military analogy of allocating rifle rounds from magazines. Each per-CPU cache has magazines of allocated objects and can allocate objects (rounds) from its own magazines without having to bother the lower layers. The CPU layer needs to allocate objects from the lower (depot) layer only when its magazines are empty. The depot layer refills magazines from the slab layer by assembling objects, which may reside in many different slabs, into full magazines.

## 6.2.4.5 The CPU Layer

The CPU layer caches groups of objects to minimize the number of times that an allocation will need to go down to the lower layers. This means that we can satisfy the majority of allocation requests without having to hold any global locks, thus dramatically improving the scalability of the allocator.

Continuing the military analogy: three magazines of objects are kept in the CPU layer to satisfy allocation and deallocation requests—a full, a half-allocated, and an empty magazine are on hand. Objects are allocated from the half-empty magazine, and until the magazine is empty, all allocations are simply satisfied from the magazine. When the magazine empties, an empty magazine is returned to the magazine layer, and objects are allocated from the full magazine that was already available at the CPU layer. The CPU layer keeps the empty and full magazine on hand to prevent the magazine layer from having to construct and deconstruct magazines when on a full or empty magazine boundary. If a client rapidly allocates and deallocates objects when the magazine is on a boundary, then the CPU layer can simply use its full and empty magazines to service the requests, rather than having the magazine layer deconstruct and reconstruct new magazines at each request. The magazine model allows the allocator to guarantee that it can satisfy at least a magazine size of rounds without having to go to the depot layer.

## 6.2.4.6 The Depot Layer

The depot layer assembles groups of objects into magazines. Unlike a slab, a magazine’s objects are not necessarily allocated from contiguous memory; rather, a magazine contains a series of pointers to objects within slabs.

The number of rounds per magazine for each cache changes dynamically, depending on the amount of contention that occurs at the depot layer. The more rounds per magazine, the lower the depot contention, but more memory is consumed. Each range of object sizes has an upper and lower magazine size. Table 6-11 shows the magazine size range for each object size.

**Table 6-11** *Magazine Sizes*

| Object Size Range | Minimum Magazine Size | Maximum Magazine Size |
|---|---:|---:|
| 0–63 | 15 | 143 |
| 64–127 | 7 | 95 |
| 128–255 | 3 | 47 |
| 256–511 | 1 | 31 |
| 512–1023 | 1 | 15 |
| 1024–2047 | 1 | 7 |
| 2048–16383 | 1 | 3 |
| 16384+ | 1 | 1 |

A slab allocator maintenance thread is scheduled every 15 seconds (controlled by the tunable `kmem_update_interval`) to recalculate the magazine sizes. If significant contention has occurred at the depot level, then the magazine size is bumped up. Refer to Table 6-12 on page 227 for the parameters that control magazine resizing.

## 6.2.4.7 The Global (Slab) Layer

The global slab layer allocates slabs of objects from contiguous pages of physical memory and hands them up to the magazine layer for allocation. The global slab layer is used only when the upper layers need to allocate or deallocate entire slabs of objects to refill their magazines.

The slab is the primary unit of allocation in the slab layer. When the allocator needs to grow a cache, it acquires an entire slab of objects. When the allocator wants to shrink a cache, it returns unused memory to the back end by deallocating a complete slab. A slab consists of one or more pages of virtually contiguous memory carved up into equal-sized chunks, with a reference count indicating how many of those chunks have been allocated.

The contents of each slab are managed by a `kmem_slab` data structure that maintains the slab’s linkage in the cache, its reference count, and its list of free buffers. In turn, each buffer in the slab is managed by a `kmem_bufctl` structure that holds the freelist linkage, the buffer address, and a back-pointer to the controlling slab.

For objects smaller than 1/8th of a page, the slab allocator builds a slab by allocating a page, placing the slab data at the end, and dividing the rest into equal-sized buffers. Each buffer serves as its own `kmem_bufctl` while on the freelist. Only the linkage is actually needed, since everything else is computable. These are essential optimizations for small buffers; otherwise, we would end up allocating almost as much memory for `kmem_bufctl` as for the buffers themselves. The free-list linkage resides at the end of the buffer, rather than the beginning, to facilitate debugging. This location is driven by the empirical observation
