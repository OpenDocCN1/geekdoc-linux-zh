dress, becomes the address in physical memory. Additional bits in the page table entry (not shown in this figure) can indicate the access permissions for that page.

![](bbox=[0.08, 0.18, 0.92, 0.72])

Figure 4.18: Mapping memory through page table

The big advantage in a paged memory system is that the pages need not map to contiguous physical memory. When a new process is loaded into memory, its size in pages must be satisfied by that number of free frames, but the frames need not be contiguous.

The *external* memory fragmentation described in Section 4.4.1 is