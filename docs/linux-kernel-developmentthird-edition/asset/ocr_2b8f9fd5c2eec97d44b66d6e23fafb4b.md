```
struct free_area   free_area[MAX_ORDER]
spinlock_t           lru_lock;
struct zone_lru {
struct list_head list;
unsigned long    nr_saved_scan;
} lru[LRU_LISTS];
struct zone_reclaim_stat reclaim_stat;
pages_scanned;
unsigned long flags;
atomic_long_t vm_stat[NR_VM_ZONE_STAT_ITEMS];
int prev_prioity;
unsigned int inactive_ratio;
wait_queue_head_t *wait_table;
unsigned long wait_table_hash_nr_entries;
unsigned long wait_table_bits;
struct pglist_data *zone_pgdat;
unsigned long zone_start_pfn;
unsigned long spanned_pages;
unsigned long present_pages;
const char *name;
};
```

The structure is big, but only three zones are in the system and, thus, only three of these structures. Let's look at the more important fields.

The lock field is a spin lock that protects the structure from concurrent access. Note that it protects just the structure and not all the pages that reside in the zone. A specific lock does not protect individual pages, although parts of the kernel may lock the data that happens to reside in said pages.

The watermark array holds the minimum, low, and high watermarks for this zone. The kernel uses watermarks to set benchmarks for suitable per-zone memory consumption, varying its aggressiveness as the watermarks vary vis-à-vis free memory.

The name field is, unsurprisingly, a NULL-terminated string representing the name of this zone. The kernel initializes this value during boot in mm/page_alloc.c, and the three zones are given the names DMA, Normal, and HighMem.

# ## Getting Pages

Now with an understanding of how the kernel manages memory—via pages, zones, and so on—let's look at the interfaces the kernel implements to enable you to allocate and free memory within the kernel.

The kernel provides one low-level mechanism for requesting memory, along with several interfaces to access it. All these interfaces allocate memory with page-sized granularity and are declared in `<linux/gfp.h>`. The core function is

```
struct page * alloc_pages(gfp_t gfp_mask, unsigned int order) *
```