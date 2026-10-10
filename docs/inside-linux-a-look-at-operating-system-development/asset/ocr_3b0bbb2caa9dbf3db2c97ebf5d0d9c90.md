# 4.4 MEMORY MANAGEMENT

lem by providing swapping and/or virtual memory.

One simple solution to a shortage of memory is to *swap out* the entire process, i.e., copy it to special storage. This swapping frees up memory which then can be used to start new programs or to swap in a previously suspended process, i.e., copy it from special storage. This special storage has in the past been smaller high-speed disk or drum storage, but nowadays is typically a reserved section of an ordinary disk.

The selection of the process to swap out or to swap in is part of a long-term scheduling decision. Such a decision is based on a process’ priority, deadline, processing category, peripheral access, etc. This is discussed further in Section 5.2.4.

A system which provides only swapping can easily find itself spending most of its I/O bandwidth saving and reloading processes and the processor will often be idle while waiting for some process to be loaded. This wait occurs because the *entire* process is moved for each swap in or swap out operation. Still, this occasional waiting is usually better than waiting for one process to finish before starting another process.

# 4.4.4 Virtual Memory

Most systems now offer some form of *virtual memory*, which is similar to swapping on a paged system. The difference is that it does not swap the entire process at one time. Instead, individual pages are loaded to memory as they are needed and they are shifted back to storage when they become inactive. It’s even possible that some pages are never loaded to memory.

Virtual memory requires some additional hardware support, specifically (1) the page table shown in Figure 4.20 needs at least one more bit in each entry of the page table to show the map is valid/invalid and (2) the processor must be able to suspend or abort and restart instructions which make reference through an invalid page. Although the first part is simple to add, the second is quite difficult, especially in light of the techniques used to extract higher performance in the processor, e.g., instruction look-ahead, out-of-order execution, etc. Almost all virtual memory systems have additional status bits associated with each page. One, called the *modify* bit (or *dirty* bit), is automatically set if the page