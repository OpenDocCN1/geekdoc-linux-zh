```
```
24 0 4 0 *     st_swmp
```
```

# Listing 7.6 q4> fields swpm_t

```
```
      Number of kthreads using this page
    0 0 2 0 u_short sm_ucnt
      Index to first free entry in this swap map
    2 0 2 0 short   sm_next
```
```

As a final bit of discussion, do you see the slight-of-hand trick played by the disk block descriptor data? How can the 28-bit field in the **dbd** point to a specific device and an offset on the device. Device numbers are 32 bits long by themselves, and the block address on a modern disk may be quite large. The smoke and mirrors employed here are several levels of indirection. The upper half of the **dbd** data, **dbd_swptb**, points to the appropriate swap table entry. Here we pick up **st_dev**, the device number, and **st_swpm**, the pointer to this chunk’s swap map. Next, the **dbd dbd_swmp** is the page offset into the swap chunk.

This means that currently no more than 2¹⁴ swap chunks may be configured on a system and that each chunk may hold only 2¹⁴ pages at most. If we do the math, this limits the maximum device swap space to:

```
```
2¹⁴ * 2¹⁴ * 4096 or 2⁴⁰ or 1 TB
```
```

# ## Summary

As we have seen, the HP-UX swap reservation policy in combination with the kernel-tunable **swapmem** feature allows the administrator control of the paging dynamics of the system. Swap is a necessary evil in many cases; it should be configured in alignment with the available memory resources and the anticipated needs of the system’s process loads.

There is another type of memory that we haven’t discussed yet: *secondary* or *non-core* memory. We are referring to our old friend, rotating magnetic disk memory. Disks provide non-volatile memory for short-term and long-term storage. The next stop on our tour of HP-UX internals is an in-depth look into the kernel file management subsystem.