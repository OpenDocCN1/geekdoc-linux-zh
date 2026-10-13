
ing store for anonymous pages of memory, so that when we are short of memory, we can copy a page out to disk and free up a page of memory.

Because swap space is used as the backing store for anonymous memory, we need to ensure we have enough swap space for the pages we may need to swap out. We do that by reserving space up-front when we create writable mappings backed by anonymous memory for heap space, stack, and writable mapped files with `MAP_PRIVATE` set.

The Solaris kernel allows us to allocate anonymous memory without reserving physical swap space when sufficient memory is available to hold the virtual contents of a process. This means that under some circumstances a system can run with little or no swap.

Traditional Unix implementations need a page-sized unit of swap space for every page-sized unit of writable virtual memory. For example, a malloc request of 8 Mbytes on a traditional Unix system would require us to reserve 8 Mbytes of swap disk space, even if that space was never used. This requirement led to the old rule of swap space = 2 × memory size—the rough assumption was that processes would, on average, have a virtual size about twice that of the physical pages they consumed. The swapfs layer allows Solaris to be much more conservative; you only need swap space for the amount of virtual memory that is larger than the pageable physical memory available in the machine.

The Solaris swap implementation uses swapfs to implement space-efficient swap allocation. The swapfs file system is a pseudo file system between the anon layer and the physical swap devices. The swapfs file system acts as if there is real swap space behind the page, even if no physical swap space was allocated.

## 5.5.2.1 Swap Allocation

Let's step back for a minute and look at how swap is allocated, and as we move through the process, we can look at how swapfs is implemented. We'll refer to swap space as seen by the segment driver as *virtual swap space*, and real (disk or file) swap space as *physical swap space*.

Swap space allocation goes through distinct stages: reserve, allocate, and swap-out. When we first create a segment, we reserve virtual swap space; when we first touch and allocate a page, we "allocate" virtual swap space for that page; then, if we have a memory shortage, we can "swap out" a page to swap space. Table 5-7 summarizes the swap states.

**Table 5-7 _Swap Space Allocation States_**

| State | Description |
|---|---|
| Reserved | Virtual swap space is reserved for an entire segment. Reservation occurs when a segment is created with private/read/write access. The reservation represents the virtual size of the area being created. |
| Allocated | Virtual swap space is allocated when the first physical page is assigned to it. At that point, a swapfs vnode and offset are assigned against the anon slot. |
| Swapped out (used swap) | When a memory shortage occurs, a page may be swapped out by the page scanner. Swap-out happens when the page scanner calls `swapfs_putpage` for the page in question. The page is migrated to physical (disk or file) swap. |

Swap space is reserved each time a heap segment is created. The amount of swap space reserved is the entire size of the segment being created. Swap space is also reserved if there is a possibility of anonymous memory being created. For example, mapped file segments that are mapped MAP_PRIVATE (e.g., the executable data segment) reserve swap space because at any time they could create anonymous memory during a copy-on-write operation.

We reserve virtual swap space up-front so that swap space allocation assignment is done at the time of request, rather than at the time of need. That way, an out-of-swap-space error can be reported synchronously during a system call. If we allocated swap space on demand during program execution rather than when we called `malloc()`, we could run out of swap space during execution and have no simple way to detect the out-of-swap-space condition. For example, in the Solaris kernel, we fail a `malloc()` request for memory as it is requested rather than when it is needed later, to prevent processes from failing during seemingly normal execution. (This strategy differs from that of operating systems such as IBM's AIX, where lazy allocation is done. If the resource is exhausted during program execution, then the process is sent a SIGDANGER signal.)

The `swapfs` file system includes all available pageable memory as virtual swap space in addition to the physical swap space. This allows us to "reserve" virtual swap space and "allocate" swap space when we first touch a page. When we reserve swap, rather than reserving disk space, we reserve virtual swap space from the `swapfs` file system. Disk swap pages are only allocated once a page is paged out.

With `swapfs`, the amount of virtual swap space available is the amount of available unlocked, pageable physical memory plus the amount of physical (disk) swap space available. If we were to run without swap space, then we would be able to reserve as much virtual memory as there is unlocked pageable physical memory available on the system. This would be fine, except that often our virtual memory requirements are bigger than our physical memory requirements, and this case would prevent us from using all of the available physical memory on the system.

For example, a process may reserve 100 Mbytes of memory and then allocate only 10 Mbytes of physical memory. The process's physical memory requirement would be 10 Mbytes, but it had to reserve 100 Mbytes of virtual swap, thus using 100 Mbytes of virtual swap allocated from our available real memory. If we ran such a process on a 128-Mbyte system, we would likely start only one of these processes before we exhausted our swap space. If we added more virtual swap space by adding a disk swap device, then we could reserve against the additional space, and we would likely get 10 or so of the equivalent processes in the same physical memory.

Another good example of a larger virtual than physical memory requirement is the process data segment. It's mapped `MAP_PRIVATE`, which means that we need to reserve virtual swap for the whole segment, but we only allocate physical memory for the few pages that we write to within the segment. The amount of virtual swap required is far greater than the physical memory allocated to it, so if we needed to swap pages out to the swap device, we would need only a small amount of physical swap space.

If we had the ideal process that had all of its virtual memory backed by physical memory, then we could run with no physical swap space. Usually, we need something like 0.5 to 1.5 times memory size for physical swap space. It varies, of course, depending on the virtual-to-physical memory ratio of the application.

## 5.5.2.2 swapfs Implementation

The `swapfs` file system uses a system global variable, `availmem`, to keep track of the available pageable physical memory in the system and adds it to the total amount of swap space available. When we reserve virtual swap, we simply decrement the amount of virtual memory available from the pool. As long as enough available memory and physical swap space are available, then the swap allocations succeed. It's not until later that physical swap space is assigned.

When we create a private segment, we reserve swap and allocate anon structures. At this stage, that's all that happens until a real memory page is created as a result of a ZFOD or copy-on-write (COW). When a physical page is faulted in, it is identified by vnode/offset, which for anonymous memory is the virtual swap device for the page.

Anonymous pages in Solaris are assigned `swapfs` vnode and offsets when the segment driver calls `anon_alloc()` to get a new anonymous page. The `anon_alloc()` function calls into `swapfs` through `swapfs_getvp()` and then calls `swapfs_getpage()` to create a new page with `swapfs` vnode/offset. The anon structure members, an_vp and an_offset, which identify the backing store for this page, are initialized to reference the vnode and offset within the `swapfs` virtual swap device.

Figure 5.13 shows how the anon slot points into `swapfs`. At this stage, we still don't need any physical swap space—the amount of virtual swap space available was decremented when the segment reserved virtual swap space—but because we haven't had to swap the pages out to physical swap, no physical swap space has been allocated.
