# 32-bit sun4u

# 64-bit sun4u

| 0xFFFBEC000 | 0xFFFFFFFF.7FFC000 |
| :--- | :--- |
| Stack | Stack |
| 0xFF3DC000 | 0xFFFFFFFF.7F7F0000 |
| Libraries | Libraries |
| | 0xFFFFFFFF.FFFFFFFF |
| | 0x00000800.00000000 |
| | VA. Hole |
| HEAP - malloc(), sbrk() | HEAP - malloc(), sbrk() |
| Executable - DATA | Executable - DATA |
| 0x00010000 Executable - TEXT | 0x00000001.00000000 |

Figure 5.5 SPARC sun4u 32- and 64-Bit Process Address Space

On all SPARC platforms, the bottom of the virtual address space is not mapped. Null pointer references will cause a segmentation fault rather than return spurious contents of whatever was at the bottom of the address space.

# 5.3.3 Intel Address Space Layout

The Intel x86 address space, like the 32-bit SPARC7 shared/kernel address space, shares the same address space for user and kernel. The main difference with the Intel address space is that the stack is mapped underneath the executable binary and grows down toward the bottom. The Intel address space is shown in Figure 5.6.

# 5.3.4 Process Memory Allocation

Process virtual memory for user data structures is allocated from the heap segment, which resides above the executable data segment. The heap starts out small and then grows in units of pages as virtual memory is allocated. It is simply a large area of virtual memory available for reading and writing. A single, large virtual memory area is difficult to program to, so a general-purpose