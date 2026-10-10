![](bbox=[0.19, 0.12, 0.85, 0.41])

**Figure 6-9 VFD/DBD**

Each and every page in a **region** has a **vfd/dbd** structure pair; these define the current status of the page. Let’s look at an annotated listing of these structures (Listings 6.7 and 6.8).

# **Listing 6.7 q4> fields struct vfd**

```
The first bit is the valid bit; it indicates that the data in the vfd is valid
0 0 0 1 u_int pg_v
The next bit sets copy-on-write access mode for a page
0 1 0 1 u_int pg_cw
When a page is locked for an I/O operation, this bit is set
0 2 0 1 u_int pg_lock
If an mlock() call has been made for a region, this bit is set
0 3 0 1 u_int pg_mlock
If lazy swap has been activated and a swap page has been reserved, this bit is set
0 4 0 1 u_int pg_swresv
On narrow systems the physical page frame number may only use 21 bits (due to the memory size limitations of 32-bit hardware). For a wide kernel, this will be a single 27-bit field
0 5 0 6 u_int pg_fill
1 3 2 5 u_int pg_pfn
```

# **Listing 6.8 q4> fields struct dbd**

The first four bits of this structure denote the page type: