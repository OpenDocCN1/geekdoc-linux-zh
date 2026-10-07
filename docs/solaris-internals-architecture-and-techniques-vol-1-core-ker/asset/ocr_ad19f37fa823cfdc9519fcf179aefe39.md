# The Hardware Address Translation Layer

# ### 5.9.1.1 Hardware Translation Acceleration

The hardware MMUs convert from virtual-to-physical addresses by looking up entries in a page translation table. All of the platforms on which Solaris runs have a hardware cache of recent translations, known as the translation buffer (TLB). The number of entries in the TLB is typically 64 on SPARC systems. Some platforms (such as Intel and older SPARC implementations) use hardware to populate the TLB, and others (like the UltraSPARC architecture) use software algorithms.

The characteristics of the MMU hardware for the different Solaris platforms are shown in Table 5-17.

**Table 5-17** Solaris MMU HAT Implementations

| Platform | No. of Contexts | Size of TLB | TLB Fill | Virtual Bits | Physical Bits |
| --- | --- | --- | --- | --- | --- |
| SPARC 1,2 | 8 | 64 | Hardware | 32 | 32 |
| MicroSPARC | 65536 | 64 | Hardware | 32 | 32 |
| SuperSPARC | 65536 | 64 | Hardware | 32 | 36 |
| UltraSPARC-I and -II | 8192 | 64 x 2 | Software | 44 | 41 |
| Intel Pentium | | | Hardware | 32 | 36 |

# ### 5.9.2 The UltraSPARC-I and -II HAT

The UltraSPARC-I and -II MMUs do the following:

+   - Implementing mapping between a 44-bit virtual address and a 41-bit physical address
- Support page sizes of 8 Kbytes, 64 Kbytes, 512 bytes, and 4 Mbytes
- Share their implementation with the entire range of UltraSPARC-based desktop and server machines, from the Ultra 1 to the Enterprise Server 10000

The MMU is an integral part of the UltraSPARC chip, which hosts two MMUs: one for instructions and one for data. Figure 5.27 illustrates the topology of the CPU and MMU.