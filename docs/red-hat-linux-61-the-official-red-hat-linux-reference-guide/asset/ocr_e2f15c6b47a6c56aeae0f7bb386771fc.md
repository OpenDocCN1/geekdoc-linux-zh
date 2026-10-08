# 56

# Chapter 5. The proc File System

Tip
To get a more readable version of this information, type:

```
/sbin/isspci -vb
```

# 5.2.26. /proc/slabinfo

This file gives information about memory usage on the slab level. Linux kernels greater than version 2.2 use slab pools to manage memory above the page level. Commonly used objects have their own slab pools. The following is a portion of a typical /proc/slabinfo virtual file:

| slabinfo - version: 1.1 |
| kmem_cache | 64 | 68 | 112 | 2 | 1 |
| nfs_write_data | 0 | | 384 | 0 | 0 |
| nfs_read_data | 0 | 160 | 0 | 16 | 1 |
| nfs_page | 0 | 200 | 96 | 5 | 1 |
| ip_filash | 10 | 113 | 32 | 1 | 1 |
| journal_head | 51 | 7220 | 48 | 2 | 1 |
| revoke_table | 2 | 253 | 12 | 1 | 1 |
| revoke_record | 0 | | 32 | 0 | 0 |
| clip_cache | 0 | | 128 | 0 | 1 |
| ip_mrt_cache | 0 | | 96 | 0 | 1 |

The values in this file follow order: cache name, number of active objects, number of total objects, size of the object, number of active slabs (blocks) of the objects, total number of slabs of the objects, and the number of pages per slab.

Note that in this case an object is in use.

# 5.2.27. /proc/stat

This file tracks a variety of different statistics about the system since it was last started. The contents of /proc/stat, which can be quite long, begins like this:

```
cpu 1139111 3689 234449 8437914
cpu0 1139111 3689 234449 8437914
page 2675248 856596
swap 10022 1926
intr 932323 8575613 174412 0 3 0 6 0 1 428620 0 60330 0 136830 5538681
disk (sda,0): (1408049,445601,5349480,962448,17135856)
ctxt 27269447
time 86490134
processes 206458
```

Some of the popular statistics include:

+   - cpu Measures the number of jiffies (one/tenth of a second) the system has been in user, user mode with low priority (nice), system mode, and in idle task, respectively. The total for all CPUs is given at the top, while each individual CPU is listed below with its out statistics.
- page The number of memory pages the system has written in and out to disk.
- swap The number of swap pages the system has brought in and out.
- intr The number of interrupts the system has experienced.