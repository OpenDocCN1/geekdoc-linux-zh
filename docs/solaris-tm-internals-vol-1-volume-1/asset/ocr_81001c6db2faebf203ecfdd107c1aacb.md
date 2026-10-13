![](bbox=[0.165, 0.133, 0.886, 0.479])

*Figure 5.27* *UltraSPARC-I and -II MMUs*

The UltraSPARC-I and -II MMU supports 44-bit virtual addresses (64 bits with a virtual address hole) and 41-bit physical addresses. During memory access, the MMU translates virtual address to physical addresses by translating a virtual page number into a physical page number and using a common page offset between the virtual and physical pages. The page number of a page is the high-order bits of the address, excluding the page offset. For 8-Kbyte pages, the page number is bits 13 through 63 of the virtual address and bits 13 through 40 of the physical address. For 4-Mbyte pages, the page number is bits 22 through 63 of the virtual address and bits 22 through 40 of the physical address.

Figure 5.28 illustrates the relationship between virtual and physical addresses.