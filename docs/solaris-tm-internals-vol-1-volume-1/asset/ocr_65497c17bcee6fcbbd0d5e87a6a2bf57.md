# ### 5.9.4.1 TLB Performance and Large Pages

The memory performance of a modern system is largely influenced by the effectiveness of the TLB because of the time spent servicing TLB misses. The objective of the TLB is to cache as many recent page translations in hardware as possible, so that it can satisfy a processor’s or thread’s memory accesses by performing all of the virtual-to-physical translations on-the-fly. If we don’t find a translation in the TLB, then we need to look up the translation from a larger table, either in software (UltraSPARC) or with lengthy hardware steps (Intel or SuperSPARC).

Most TLBs are limited in size because of the amount of transistor space available on the CPU die. For example, the UltraSPARC-I and -II TLBs are only 64 entries. This means that the TLB can at most address 64 pages of translations at any time; on UltraSPARC, 64 × 8 Kbytes, or 512 Kbytes.

The amount of memory the TLB can address concurrently is known as the TLB reach, so we can say the UltraSPARC-I and -II have a TLB reach of 512 Kbytes. If an application makes heavy use of less than 512 Kbytes of memory, then the TLB will be able to cache the entire set of translations. But if the application were to make heavy use of more than 512 Kbytes of memory, then the TLB will begin to miss, and translations will have to be loaded from the larger translation table.

Table 5-22 shows the TLB miss rate and the amount of time spent servicing TLB misses from a study done by Madu Talluri [36] on older SPARC architectures. We can see from the table that only a small range of compute-bound applications fit well in the SuperSPARC TLB (gcc, ML, and pthor), whereas the others spend a significant amount of their time in the TLB miss handlers.

**Table 5-22. _Sample TLB Miss Data from a SuperSPARC Study_**

| Workload | Total Time (secs) | User Time (secs) | # User TLB Misses | % User Time in TLB Miss Handling | Cache Misses ('000s) | Peak Memory Usage (MB) |
|---|---:|---:|---:|---:|---:|---:|
| coral | 177 | 172 | 85974 | 50 | 71053 | 19.9 |
| nasa7 | 387 | 385 | 152357 | 40 | 64213 | 3.5 |
| compress | 99 | 77 | 21347 | 28 | 21567 | 1.4 |
| fftpde | 55 | 53 | 11280 | 21 | 14472 | 14.7 |
| wave5 | 110 | 107 | 14510 | 14 | 4583 | 14.3 |
| mp3d | 37 | 36 | 4050 | 11 | 5457 | 4.8 |
| spice | 620 | 617 | 41923 | 7 | 81949 | 3.6 |
| pthor | 48 | 35 | 2580 | 7 | 6957 | 15.4 |
| ML | 945 | 917 | 38423 | 4 | 314137 | 32.0 |
| gcc | 118 | 105 | 2440 | 2 | 9980 | 5.6 |

TLB effectiveness has become a larger issue in the past few years because the average amount of memory used by applications has grown significantly—by as