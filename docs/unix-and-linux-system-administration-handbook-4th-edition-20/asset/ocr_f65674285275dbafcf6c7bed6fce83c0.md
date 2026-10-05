# Chapter 29 Performance Analysis

Chapter 24, Virtualization, for additional information about various virtualization technologies and their implications.

# How the system manages memory

The kernel manages memory in units called pages that are usually 4KiB or larger. It allocates virtual pages to processes as they request memory. Each virtual page is mapped to real storage, either to RAM or “backing store” on disk. (Backing store is usually in the swap area, but for pages that contain executable text, the backing store is the original executable file. For some data files it may be the files themselves.) The kernel uses a “page table” to keep track of the mappings between these made-up virtual pages and real pages of memory.

The kernel can effectively allocate as much memory as processes ask for augmenting RAM with swap space. Since processes expect virtual pages to map to real memory, the kernel may have to constantly shuffle pages between RAM as different pages are accessed. This activity is known as paging.

The kernel tries to manage the system’s memory so that pages that have been recently accessed are kept in memory and less pages are pushed out to disk. This scheme is an LRU system since the least recently used pages are the ones that get shunted to disk.

It would be inefficient for the kernel to keep track of all memory references, so it uses a cache-like algorithm to decide which pages to keep in memory. The algorithm varies by system, but the concept is similar across platforms. This system is cheaper than a true LRU system and produces comparable results.

When memory is low, the kernel tries to guess which pages on the inactive list were least used. If those pages have been modified by a process, they are considered “dirty” and must be pushed out to disk before the memory can be reused. Pages that have been laundered in this fashion (or were never dirty to begin with) are “clean” and can be recycled for use elsewhere.

When a process refers to a page on the inactive list, the kernel returns the page’s memory mapping to the page table, resets the page, and transfers it from the inactive list to the active list. Pages that have been written to disk must be pushed in before they be reactivated if the page in memory has been remapped. A “soft fault” occurs when a process references an in-memory inactive page and a “hard fault” results from a reference to a nonresident (p-out) page. In other words, a hard fault requires a page to be read from disk and a soft fault does not.

The kernel tries to stay ahead of the system’s demand for memory, so there is not necessarily a one-to-one correspondence between page-out events and page allocations by running processes. The goal of the system is to keep free

+   3. Ages, a second process known as “swapping” could occur by which all pages of a process were pushed out to disk at the same time. Today, demand paging is used in all cases.