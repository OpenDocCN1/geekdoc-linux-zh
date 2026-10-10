![](bbox=[0.05, 0.1, 0.9, 0.48])

The `pfn_to_virt_ptr` structure merely directs us to the appropriate page partition table that contains the actual `pfn_to_virt_entry` structures. The granularity of the partitioning is determined by the kernel parameter PFN_CONTIGUOUS_PAGES (currently default to 4096). To find the correct `pfn_to_virt_entry`, we need to divide the physical page number by 4096 to find an index and offset (the remainder). First, we index into `pfn_to_virt_ptr` and find the pointer to the `pp_tbl` structure containing our `pfn_to_virt_entry`. The remainder is our index into the `pp_tbl`. Let's take a look at an annotated listing of these two structures (Listings 6.3 and 6.4).

```
Listing 6.3 q4> fields struct pfn_to_virt_ptr

The pp_tbl points to a block of "page frame number to virtual" entries and the pp_offset directs us to the first valid entry in the block. Each block maps 4096 physical page translations (determined by the kernel parameter PFN_CONTIGUOUS_PAGES)

```
 0 0 4 0 *  pp_tbl
 4 0 4 0 int pp_offset
```
```

```
Listing 6.4 q4> fields struct pfn_to_virt_entry

The first word of each entry contains either the virtual space number or INVALID_SPACE_ENTRY (0xffffff). The second word is either the page offset or a pointer to an alias structure

```
 0 0 4 0 u_int space
 4 0 4 0 u_long alias_or_offset.offset_page
 4 0 4 0 *     alias_or_offset.alias
```
```