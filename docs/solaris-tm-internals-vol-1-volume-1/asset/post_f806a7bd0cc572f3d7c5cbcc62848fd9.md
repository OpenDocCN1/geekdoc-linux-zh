
## 5.9.1.1 Hardware Translation Acceleration

The hardware MMUs convert from virtual-to-physical addresses by looking up entries in a page translation table. All of the platforms on which Solaris runs have a hardware cache of recent translations, known as the translation lookaside buffer (TLB). The number of entries in the TLB is typically 64 on SPARC systems. Some platforms (such as Intel and older SPARC implementations) use hardware to populate the TLB, and others (like the UltraSPARC architecture) use software algorithms.

The characteristics of the MMU hardware for the different Solaris platforms are shown in Table 5-17.

**Table 5-17** *Solaris MMU HAT Implementations*

| Platform | No. of Contexts | Size of TLB | TLB Fill | Virtual Bits | Physical Bits |
|---|---:|---:|---|---:|---:|
| SPARC 1, 2 | 8 | 64 | Hardware | 32 | 32 |
| MicroSPARC | 65536 | 64 | Hardware | 32 | 32 |
| SuperSPARC | 65536 | 64 | Hardware | 32 | 36 |
| UltraSPARC-I and -II | 8192 | 64 x 2 | Software | 44 | 41 |
| Intel Pentium |  |  | Hardware | 32 | 36 |

## 5.9.2 The UltraSPARC-I and -II HAT

The UltraSPARC-I and -II MMUs do the following:

- Implement mapping between a 44-bit virtual address and a 41-bit physical address
- Support page sizes of 8 Kbytes, 64 Kbytes, 512 Kbytes, and 4 Mbytes
- Share their implementation with the entire range of UltraSPARC-based desktop and server machines, from the Ultra 1 to the Enterprise Server 10000

The MMU is an integral part of the UltraSPARC chip, which hosts two MMUs: one for instructions and one for data. Figure 5.27 illustrates the topology of the CPU and MMU.

![](img/220ae4af07df2fe8e5be69d27f885d1b_235_0.png)

**Figure 5.27** *UltraSPARC-I and -II MMUs*

The UltraSPARC-I and -II MMU supports 44-bit virtual addresses (64 bits with a virtual address hole) and 41-bit physical addresses. During memory access, the MMU translates virtual address to physical addresses by translating a virtual page number into a physical page number and using a common page offset between the virtual and physical pages. The page number of a page is the high-order bits of the address, excluding the page offset. For 8-Kbyte pages, the page number is bits 13 through 63 of the virtual address and bits 13 through 40 of the physical address. For 4-Mbyte pages, the page number is bits 22 through 63 of the virtual address and bits 22 through 40 of the physical address.

Figure 5.28 illustrates the relationship between virtual and physical addresses.

![8-Kbyte Page](img/220ae4af07df2fe8e5be69d27f885d1b_236_0.png)

4-Mbyte Page

**Figure 5.28** *Virtual-to-Physical Translation*

We traditionally use page tables to map virtual-to-physical addresses, so that for any given virtual address, the MMU hardware looks up and translates the appropriate physical address. microSPARC and SuperSPARC processors use page tables for address translation to convert virtual page numbers to physical page numbers. The microSPARC and SuperSPARC page table comprises mapping entries, one per page, known as *page table entries*, that map each virtual page to a physical page.

In UltraSPARC-I and -II, we use a translation table to describe the virtual-to-physical translation. A translation table is the functional equivalent of a page table, with some significant differences. For example, unlike the older page table implementation (like that on SuperSPARC), the UltraSPARC-I and -II MMU uses a software-assisted translation mechanism to fill the hardware TLB translation cache.

The UltraSPARC-I and -II software page table entries are known as translation table entries (TTEs), one TTE for each page. The TTE is a translation map entry that contains a virtual address tag and the high bits of the physical address for each page (the physical page number) so that the hardware MMU can convert the virtual page address into a physical address by finding entries matching the virtual page number.

The TTE virtual page tag contains the virtual page number of the virtual address it maps and the address space context number to identify the context to which each TTE belongs. The context information in the TTE allows the MMU to find a TTE specific to an address space context, which allows multiple contexts to be simultaneously active in the TLB. This behavior offers a major performance benefit because traditionally we need to flush all the TTEs for an address space when we context-switch. Having multiple TTE contexts in the TLB dramatically decreases the time taken for a context switch because translations do not need to be reloaded into the TLB each time we context-switch.

The TTEs found in the page structure are a software representation of the virtual-to-physical mapping and must be loaded into the TLB to enable the MMU to perform a hardware translation. Once a TTE is loaded, the hardware MMU can translate addresses for that TTE without further interaction. The hardware MMU relies on the hardware copies of the TTEs in the TLB to do the real translation. The TLB contains the 64 most recent TTEs and is used directly by the hardware to assemble the physical addresses of each page as virtual addresses are accessed.

The MMU finds the TTE entry that matches the virtual page number and current context. When it finds the match, it retrieves the physical page information. The physical page information contains the physical page number (which is the high-order bits of the physical address, bits 40:13 or 40:22), the size of the page, a bit to indicate whether the page can be written to, and a bit to indicate whether the page can only be accessed in privileged mode.

Figure 5.29 illustrates how TTEs are used.

| Virtual Page Tag | Physical Page |
|---|---|
| Virtual Page Number<br>Context Number (0–8191) | Physical Address (Bits 40:13)<br>Page Size<br>Valid Bit<br>Protected Page Bit<br>Writable Page Bit |

**Figure 5.29** *UltraSPARC-I and -II Translation Table Entry (TTE)*

Software populates the TLB entries from the hment structures in the machine-specific page structure. Since the process of converting a software TTE into a TLB entry is fairly expensive, an intermediate software cache of TTEs is arranged as a direct-mapped cache of the TLB. The software cache of TTEs is the translation software buffer (TSB) and is simply an array of TTEs in regular physical memory. Figure 5.30 shows the relationship between software TTEs, the TSB, and the TLB.

![](img/220ae4af07df2fe8e5be69d27f885d1b_238_0.png)

**Figure 5.30** *Relationship of TLBs, TSBs, and TTEs*

The TLB on UltraSPARC-I and -II has 64 entries, and the TSB has between 2,048 and 262,144 entries, depending on the amount of memory in the system. Unlike the previous generation SPARC MMU, the UltraSPARC-I and -II MMU does not use a hardware page tablewalk to access the TSB entries, but it still provides a form of hardware assistance to speed up TSB access: hardware precomputes TSB table offsets to help the software handler find TTEs in the TSB. When the CPU needs to access a virtual address, the system takes the following steps:

1. The MMU first looks in the TLB for a valid TTE for the requested virtual address.
2. If a valid TTE is not found, then the MMU automatically generates a pointer for the location of the TSB TTE entry and generates a TLB miss trap.
3. The trap handler reads the hardware-constructed pointer, retrieves the entry from the TSB, and places it in the appropriate TLB slot with an atomic write into the TLB.
4. If the TTE is not found in the TSB, then the TLB miss handler jumps to a more complex, but slower, TSB miss handler, which retrieves the TTE from the page structure by using a software hashed index structure.

UltraSPARC-I and -II also provide a separate set of global registers to process MMU traps. This approach dramatically reduces the time taken for the TLB miss handler to locate TSB entries since the CPU does not need to save process state during the trap—it simply locates the entry, atomically stores the entry, and returns to execution of the running process.
