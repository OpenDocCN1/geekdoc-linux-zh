
- Find the page’s buddy. This is a simple task of changing the bit corresponding to the page’s current size and checking whether it is free.
- Confirm that the page to be freed and its buddy are in the same pond.
- Coalescence is only attempted for pages in the cached pond if at least one-third of the pond’s pages are currently free. In the case of uncached pages, coalescence is always attempted.
- The resulting page (coalesced if possible) is then placed at the end of the appropriate free list.

## Summary

  We have seen the four primary views of memory managed by the kernel and utilized by the process threads and PA-RISC hardware. All of the various levels of abstraction would be pointless if we couldn’t allocate physical memory when it was time to allow a thread to run.

  Having an ample supply of free pages is very important to overall system performance. To this end the kernel employs a swapping or paging system. We examine it next.

# CHAPTER 7

# The HP-UX Paging System

  Classic UNIX featured a program swapping system. When the kernel needed to make room in-core memory for a process to run, it would select an inactive process or one of a lesser priority and move it from physical memory to a temporary storage location on disk. The program was then said to be *swapped out*. Before the process could run again, it would have to be swapped back into memory. This could tie up a large portion of the system's I/O bandwidth. Whole process swapping has been relegated to the history books; modern kernels utilize a *demand paging system*.

## Pages on Demand

  In a demand paging system, instead of loading all of a program's text and data at the time the program is dispatched, the system waits for a page to fault and then loads only the required page. This means that at any specific point only a small portion of a process's pages need be resident in physical memory. All first references to a page result in a page fault, but if a system has ample memory then eventually all of a process's pages will be mapped to physical pages and performance will be optimal. If the demand for pages exceeds the system's configured or available memory, then pages will have to be paged out before others may be paged in.

  The HP-UX paging system is responsible for loading pages when they are first requested and monitoring and maintaining a reasonable supply of free pages. If the amount of free memory drops below tunable system thresholds, the paging system must identify pages to be paged out. Page-ins will always occur; at least as long as new programs are dispatched, but significant numbers of page-outs indicate memory pressure has increased and overall system performance will begin to diminish. This is not necessarily bad; it is just a case of cause and effect that the system administrator must understand.

  When a page fault occurs, the kernel must be able to identify the location of the requested page and take corrective action. As we saw in Chapter 6, “Managing Memory,” in our discussion of the **ddb**, each nonce resident page is typed. The paging system understands the various types and how to recover them. Let’s look at the types in detail.

### Faulting in a Page from Front Store

  A requested page may be part of a process’s text image or an initialized data page. If so, the appropriate page is found in the program file, and it is loaded to a free page frame. In addition to scheduling the page-in, the kernel must update the **hash**, **region**, **pfdat**, and **pfn_to_virt** table entries as well.

  The routine handles read-ahead page requests as well: the **p_pagein** in the **preregion** is adjusted according to whether the file is being accessed in a random or sequential manner, which is determined by monitoring the address of faulting pages. Each time a fault is handled for a region, its **p_nextfault** is set to the next sequential page address following the one that caused the current fault (the current faulting page number plus **p_pagein**). When the next fault for this **preregion** occurs, the faulting page address is compared to this value. If it matches, we are performing sequential reads, in which case **p_pagein** is multiplied by 2 (the value is limit-checked against the kernel’s **maxpagein_size**, default is 64). If **p_strength** is less than 100 and we have detected a sequential operation, it is incremented. This gives us a sense of how sequential our access is.

  If the next fault is not sequential, **p_pagein** is divided by 2 (limit-checked against **minpagein_size**, defaults to 1), and the **p_strength** is decremented unless it is currently equal to $-100$.

  From the above description we can see that **p_strength** may vary between $-100$ (defined as **PURELY_RANDOM**) and $+100$ (defined as **PURELY_SEQUENTIAL**), and **p_pagein** may vary by powers of two between 1 and 64.

### Faulting in a Page from Back Store (Swap)

  A page may currently reside in swap. Before the page is scheduled for a page-in, the system first calls **vm_no_io_required()** to check the **pash** in case the page was swapped but never revalidated. If this is the case, the page is still in memory and all the kernel has to do is update the tables—no actual page-in is required. This is called a *soft page fault*. If the fault is not soft, then a page-in is scheduled and the four tables are updated as in the previous case.

### Faulting in a Zero-Fill Page

  If the page requested is a uninitialized data page, the kernel simply has to find a free page, fill it with zeros, and update the four tables. Uninitialized data pages are also known as block store by symbol (**BSS**) pages and constitute the majority of a process’s private data area.

### Faulting in a No-Fill Page

  In addition to these three types of pages, the kernel may be asked to fault in a no-fill page. This is similar to the BSS page fault except that we don’t fill the page with zeros. The page will still contain whatever residue was left behind by its previous owner. For this reason, this option is available only for pages being allocated for kernel use and, in particular, only for use as `uarea` pages. The `uarea` is not visible to the process, only to the kernel so residue data is not subject to examination by a user thread.

### Digging a Memory Hole

  The final type is a page called a *memory hole*, used for linkage to sparse memory-mapped files. When a read is scheduled against one of these pages, a requestor receives a 0 or null value; when a write is attempted, the semantics of the zero-fill page are followed.

## Monitoring Free Memory

  Maintaining an ample supply of free pages for the system is a key duty of the kernel; to this end, the kernel symbol `freeemem` contains the total number of page frames currently on a free list. When memory pressure is high, there are relatively few free pages on the free lists, and the kernel must take corrective action. Figure 7-1 gives us an overall view of the free-page monitoring system.

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_222_0.png)

  The total amount of memory available to the operating system is determined at boot and stored in the kernel parameter `phys_mem_pages`. Additional setpoints are calculated and continuously monitored by the kernel.

### lotsfree

  The tunable parameter `lotsfree` sets the point at which the paging system is first called into action. If the number of free pages, `freemem`, is above `lotsfree`, then the paging system has nothing to do. The default value for `lotsfree` depends on the amount memory configured for the system.

  For systems with 32 MB to 2 GB of physical memory, `lotsfree` will be 1/16 of the non-kernel memory, not to exceed 8192 pages (32 MB). For systems with more than 2 GB, `lotsfree` is set to 16,384 pages (64 MB).

### desfree

  The tunable parameter `desfree` sets the minimum desired number of free system pages. When the number of free pages drop below this limit, the `vhand` agents are already working at their maximum rate. The swapper starts evaluating processes for potential deactivation, but no deactivations take place yet.

  For systems with 32 MB to 2 GB of memory, `desfree` is set to 1/64 of non-kernel memory, not to exceed 1024 pages (4 MB). For systems with more than 2 GB of memory, `desfree` is set to 3072 pages (12 MB).

### minfree

  When the tunable parameter `minfree`'s limit is hit, things are really tight. supply is not keeping up with demand by any stretch of the imagination. In terms of memory availability, we are in the 11th hour, so the kernel asks the swapper to start process deactivations. Hopefully, this action will get `freemem` back into an acceptable range.

  For systems with 32 MB to 2 GB of memory, `minfree` is set to 1/4 of `desfree`, not to exceed 256 pages. For systems with more than 2 GB of memory, `minfree` is set to 1280 pages (5 MB).

### gggslim

  At boot time, this parameter is set to 1/4 of the way between `desfree` and `lotsfree`. When `freemem` drops below `lotsfree`, the `vhand` daemon is started, but at this time it only ages pages—no stealing is done. If `freemem` drops below `gggslim`, then the other half of `vhand` is activated, and it steals stale pages. The kernel adjusts `gggslim` between `lotsfree` and `desfree` in accordance with recent current trends in memory pressure. (In earlier versions of HP-UX this parameter was tunable.)
