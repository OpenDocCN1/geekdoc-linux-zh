# 5.8.3 Shared optimization

A subtle optimization added to the page scanner prevents it from stealing pages from extensively shared libraries. The page scanner looks at the share reference count for each page; if the page is shared more than a certain amount, then it is skipped during the page scan operation. An internal parameter, po_share, sets the threshold for the amount of shares a page can have before it is skipped. If the page has more than po_share mappings (i.e., it shared by more than po_share processes), by default, po_share starts at 8; each time around, it is decremented unless the scan around the clock does not find any page to free, in which case po_share is incremented. The po_share parameter can float between 8 and 134217728.

# 5.8.4 The Priority Paging Algorithm

Solaris 7 shipped with a new optional paging algorithm—a page-stealing algorithm that results in much better system response and throughput for systems using of the file systems. The algorithm is also available on older Solaris releases (from 2.5.1 onwards) with the addition of a kernel patch. You enable the new algorithm by setting the priority_paging variable to 1 in /etc/system.

+   * Enable the Priority Paging Algorithm
* set priority_paging = 1

The new algorithm was introduced to overcome adverse behavior that results from the memory pressure caused by the file system. In SunOS 4.0, the virtual memory system was rewritten, the file system cache and virtual memory system were integrated to allow the entire memory system to be used as a file system cache; that is, the file system uses pages of memory from the free memory pool, just as processes do when they request memory.

The demand paging algorithm allows the file system cache to grow and shrink dynamically by stealing pages that have not been recently used by other subsystems. However when this work was done, the memory pressure from the file system was relatively low, as the memory requests from the processes were on. Both were in the order of tens to hundreds of pages per second, so memory allocation could be based on who was using the pages most. When processes accessed their memory pages frequently, the scanner was biased to steal from the file system, and the file system cache would shrink accordingly.

Today, systems are capable of sustaining high I/O rates, which means that the file system can put enormous memory pressure on the memory system—so much that the amount of memory pressure from the file system can completely destroy application performance by causing the page scanner to steal many processes.