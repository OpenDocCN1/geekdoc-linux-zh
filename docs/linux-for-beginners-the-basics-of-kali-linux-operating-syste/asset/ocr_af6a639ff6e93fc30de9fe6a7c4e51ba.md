+   * Memory protection. Addressing errors that occur in a process code should only affect the execution of that process. When the P2 process does a write operation at 0x7500, it must be interrupted by an error. The memory security strategy is that a valid address range is stored for each process, and each memory access operation is checked for an address belonging to that range

+   * Lack of binding to physical memory addresses. The process can be performed regardless of its memory location and physical memory size. The process address space is allocated as a large static address set, with each address of the set being moved. Processor and hardware should be able to convert these addresses to physical addresses of main memory (the same address placeable at different times or for different processes may correspond to different places including his address))

# # The Concept Of Virtual Memory

Virtual memory - a technology that introduces I level additional conversions between memory addresses used by the process and physical memory addresses used by the desktop app. Such transformations should ensure that the memory is protected and that the process is not bound to physical memory addresses.

With virtual memory, the physical memory of the process address space can be fragmented, since the bulk of the memory occupied by the process remains free most of the time. There is a so-called ninety to ten rule or a localization rule that states that 90% of memory accesses in the process account for 10% of its address space. You can move the addresses so that only the sections of the process address space that are actually in use at that time correspond to the main memory.

In this case, unused partitions of the address space can be mapped to slower memory, such as hard disk space, and at this time other processes can use the main memory, which previously displayed the