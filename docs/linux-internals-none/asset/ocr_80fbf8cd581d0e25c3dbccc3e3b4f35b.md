# The Least Recently Used (LRU) Algorithm

Linux uses the LRU algorithm to decide which pages are to be selected for page out. The LRU implementation in Linux is pretty much based on common knowledge in OS theory. There is a variable, `lru_page`, that points to the head of the LRU. Each time a page gets added to any kind of freeable cache (so that `shrink_mmap` may later need to shrink when the memory gets low) the page is queued at one end of the LRU list. At the other end, `shrink_mmap` tries to release the pages. A reference bit of aging is involved in this process, to avoid the cost of rolling the list at each cache hit. All the LRU handling is SMP threaded and allows the VM to shrink the cache even while another CPU is querying on the page cache.

# Swapping and Discarding Pages

When memory becomes scarce, the Linux memory management subsystem attempts to free physical pages. This function is performed by the kernel swap daemon (*kswapd*). The name *swap daemon* is a bit of a misnomer, because the daemon does more than just swap modified pages out to the swap file. Its task is to keep the memory management system operating efficiently. `kswapd` is started by the kernel `init` process at startup time, and sits waiting for the kernel swap timer to periodically expire. Awakened by the VM manager every time the timer expires, `kswapd` looks to see if the number of free pages in the system is getting too low.

The main function of `kswapd` is to provide free memory for atomic allocations. These happen inside interrupt context and can’t sleep, because they need to be fast in order not to hurt IRQ or soft IRQ latency. The `kswapd` daemon is an autonomous kernel thread whose only task is to infinitely run the `kswapd()` function in `mm/vmscan.c`. The `kswapd` daemon typically sleeps on the `kswapd_wait` wait queue. It is awakened by the zone allocator if memory pressure within a given zone (or globally) goes above a given threshold; `kswapd()` then tries to free pages so that memory pressure returns to the proper low state. That’s all it does.

Freeing pages is a complex task that involves five steps:

+   1. Try to free “clean” pages (page cache, buffer cache).