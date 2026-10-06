# Chapter 10 • PROVIDING HIGH AVAILABILITY IN YOUR UNIX SYSTEM 263

# Resynchronizations Happen Automatically

Most RAID-1 implementations will resynchronize replaced disks automatically, without any user intervention. The resynchronization is usually incremental to save time. If for some reason you require a full resynchronization, you would have to invoke that manually whatever RAID hardware or software is controlling the mirror.

RAID-1 does involve additional costs: For every disk that contains data, you need at least one additional disk for the mirror. This makes RAID-1 the most expensive RAID option. So plan to spend twice as much on disks as you would without mirroring. Figure 10.8 shows how data is mirrored across two disks in a RAID-1 mirror.

# FIGURE 10.8

A two-way RAID-1 mirror duplicates data on each disk.

| 110010 | 110010 |
|--- |--- |
| 101011 | 101011 |
| 001010 | 001010 |
| 000011 | 000011 |
| 101010 | 101010 |
| 111100 | 111100 |

# RAID-4

Error correction is another effective method of redundancy. Error correction provides the same level of redundancy as mirroring, but it uses methods like checksums or parity bits to recalculate missing data. RAID-4 is an extension of RAID-0 that adds a dedicated parity bit to recover over containing actual data (data disks).

When writes are made to the data disks, the RAID-4 subsystem calculates parity for each stripe and stores it on the parity disk. When a disk fails or is removed, the missing data on that disk is re-created using existing data disks and the parity information. This condition is called "degraded mode" because both the redundancy and performance of the RAID-4 volume are degraded. Fortunately, you can designate individual disks as spares that take over for failed disks; the data on the failed disk is easily rebuilt from the parity and rewritten to the space. Once the rebuild is complete, the RAID-4 array regains its full performance and redundancy. Figure 10.9 illustrates a RAID-4 arrangement.

# FIGURE 10.9

RAID-4 requires separate data and parity disks. The bits on the parity disk are calculated using XOR operations on the data bits.

| 1011 | XOR | 1001 | = | 0010 |
|--- |--- |--- |--- |--- |
| 0001 | XOR | 1111 | = | 1110 |
| 0101 | XOR | 0101 | = | 0000 |
| 1110 | XOR | 0011 | = | 1101 |

| Disk 1 (Data) | Disk 2 (Data) | Disk 3 (Parity) |