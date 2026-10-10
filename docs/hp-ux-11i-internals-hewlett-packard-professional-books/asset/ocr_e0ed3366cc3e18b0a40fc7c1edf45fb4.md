![](bbox=[0.15, 0.1, 0.85, 0.45])

*pfdat_ptr* partition size is set by **PFN_CONTIGUOUS_PAGES** and currently defaults to 4096 pages, or 16 MB, of contiguous memory. Only those physical page frames that may be dynamically paged in or out by the kernel have *pfdat* structures. The kernel’s static pages do not require inclusion in this table, as they will never be part of the dynamic memory pool.

The two-tier nature of this structure makes it easy to skip blocks of memory pages such as kernel static memory pages or holes in the physical hardware map. In *pfdat_ptr*, a **pp_tbl** set to zero simply means that the corresponding 16-MB block of memory is not dynamically mapped. Note, this does not mean that the memory does not physically exist, just that it is not to be managed by this structure. (See Listing 6.11.)

# Listing 6.11 **q4_fields** struct **pfdat_ptr**

```
The pp_tbl points to a block of "page free data" entries and the pp_offset directs us to the first valid entry in the block. Each block maps 4096 physical page translations (determined by the kernel parameter PFN_CONTIGUOUS_PAGES)
0 0 4 0 * pp_tbl
4 0 4 0 int pp_offset
```

Once we have used the physical page number and have followed the appropriate *pp_tbl* pointer, we will find the page’s *pfdat* data structure. Let’s examine an annotated listing of this structure (Listing 6.12).