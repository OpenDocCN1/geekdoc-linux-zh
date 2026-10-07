# Table 5-16 Machine-Independent HAT Functions

| Function | Description |
|--- | --- |
| hat_alloc() | Allocates a HAT structure in the address space. |
| hat_chgattr() | Changes the protections for the supplied virtual address range. |
| hat_clrattr() | Clears the protections for the supplied virtual address range. |
| hat_free_end() | Informs the HAT layer that a process has exited. |
| hat_free_start() | Informs the HAT layer that a process is exiting. |
| hat_get_mapped_size() | Returns the number of bytes that have valid mappings. |
| hat_getattr() | Gets the protections for the supplied virtual address range. |
| hat_memload() | Creates a mapping for the supplied page virtual address. Used to create mappings. |
| hat_setattr() | Sets the protections for the supplied virtual address range. |
| hat_stats_disable() | Finishes collecting stats on an address space. |
| hat_stats_enable() | Starts collecting page reference and modification stats on an address space. |
| hat_swapin() | Allocates resources for a process that is about to be swapped in. |
| hat_swapout() | Allocates resources for a process that is about to be swapped out. |
| hat_sync() | Synchronizes the struct_page software referenced and modified bits with the hardware MMU. |
| hat_unload() | Unloads a mapping for the given page at the address. |

#  5.9.1 Virtual Memory Contexts and Address Spaces

A virtual memory context is a set of virtual-to-physical translations that maps an address space. We change virtual memory contexts when the scheduler wants to switch execution from one process to another or when a trap or interrupt from user to kernel mode occurs. The Solaris kernel uses virtual memory zero to indicate the kernel context. The machine-specific HAT layer functions required to create, delete, and switch virtual memory contexts. Different hardware MMUs support different numbers of concurrent virtual memory contexts.

When the number of concurrent address spaces (processes) exceeds the number of concurrent contexts supported by the hardware, the kernel has to steal contexts from peer processes at the time of context switch. Stealing contexts from other address spaces has an indirect effect on performance. However, this issue was only on older systems such as the SPARCstation 1 and 2.