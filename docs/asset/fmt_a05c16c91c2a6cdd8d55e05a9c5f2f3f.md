
# Page Cache Structure and Flags

* Try to keep the most commonly accessed fields in single cache lines here (`16 bytes or greater`). This ordering should be particularly beneficial on `32-bit` processors.
* The first line is data used in page cache lookup, the second line is used for linear searches (`eg. clock algorithm scans`).

## Page Structure Definition

```c
typedef struct page {

    struct list_head list;

    struct address_space *mapping;

    unsigned long index;

    struct page *next_hash;

    atomic_t count;

    unsigned long flags;      /* atomic flags, lost possibly updated asynchronously */

    struct list_head lru;

    wait_queue_head_t wait;

    struct page **prev_hash;

    struct buffer_head * buffers;

    unsigned long virtual; /* nonzero if kmapped */

    struct zone_struct *zone;

} mem_map_t;
```

## Page Reference Count Macros

```c
#define get_page(p)         atomic_inc(&(p)->count)

#define put_page(p)         __free_page(p)

#define put_page_testzero(p)        atomic_dec_and_test(&(p)->count)

#define page_count(p)       atomic_read(&(p)->count)

#define set_page_count(p,v)         atomic_set(&(p)->count, v)
```

## Page Flag Bit Values

```c
#define PG_locked           0

#define PG_error            1

#define PG_referenced  2

#define PG_uptodate     3

#define PG_unused_00   4

#define PG_decr_after  5

#define PG_unused_01   6

#define PG_unused_02   7

#define PG_slab        8

#define PG_swap_cache  9

#define PG_skip       10

#define PG_swap_entry 11

#define PG_highmem    12

                  /* bits 21-30 unused */

#define PG_reserved   31
```

## Page Flag Operations

```c
#define PageUptodate(page)    test_bit (PG_uptodate, &(page)->flags)

#define SetPageUptodate(page) set_bit(PG_uptodate, &(page)->flags)

#define ClearPageUptodate(page) clear_bit(PG_uptodate, &(page)->flags)

#define PageLocked(page)      test_bit(PG_locked, &(page)->flags)

#define LockPage(page)        set_bit(PG_locked, &(page)->flags)

#define TryLockPage(page)     test_and_set_bit(PG_locked, &(page)->flags)

#define UnlockPage(page)      do { \
                             clear_bit(PG_locked, &(page)->flags); \
                             wake_up(&(page)->wait); \
                        } while (0)

#define PageError(page)       test_bit(PG_error, &(page)->flags)

#define SetPageError(page)    test_and_set_bit(PG_error, &(page)->flags)

#define ClearPageError(page)  clear_bit(PG_error, &(page)->flags)

#define PageReferenced(page)  test_bit(PG_referenced, &(page)->flags)

#define PageDecrAfter(page)   test_bit(PG_decr_after, &(page)->flags)

#define PageSlab(page)        test_bit(PG_slab, &(page)->flags)

#define PageSwapCache(page)   test_bit(PG_swap_cache, &(page)->flags)

#define PageReserved(page)    test_bit(PG_reserved, &(page)->flags)

#define PageSetsSlab(page)    set_bit(PG_slab, &(page)->flags)

#define PageSetsSwapCache(page) set_bit(PG_swap_cache, &(page)->flags)

#define PageTestandSetSwapCache(page) test_and_set_bit(PG_swap_cache, &(page)->flags)

#define PageClearSlab(page) clear_bit(PG_slab, &(page)->flags)

#define PageClearSwapCache(page) clear_bit(PG_swap_cache, &(page)->flags)

#define PageTestandClearSwapCache(page) test_and_clear_bit(PG_swap_cache, &(page)->flags)

#ifdef CONFIG_HIGHMEM

#define PageHighMem(page) test_bit(PG_highmem, &(page)->flags)

#else

#define PageHighMem(page) 0 /* needed to optimize away at compile time */

#endif

#define SetPageReserved(page) set_bit(PG_reserved, &(page)->flags)

#define ClearPageReserved(page) clear_bit(PG_reserved, &(page)->flags)
```

## Error Return Values

```c
#define NOPAGE_SIGBUS (NULL)

#define NOPAGE_OOM ((struct page *) (-1))
```

* `PG_reserved` is set for a page which must never be accessed (`which may not even be present`).
* `PG_DMA` has been removed, `page->zone` now tells exactly whether the page is suited to do `DMAing` into.
* Multiple processes may "see" the same page. `E.g. for untouched`
