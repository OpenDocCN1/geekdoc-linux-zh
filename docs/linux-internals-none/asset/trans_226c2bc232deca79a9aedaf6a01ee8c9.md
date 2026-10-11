
## Linux 虚拟机管理器

```c
struct vm_area_struct * vm_avl_right;
/* For areas with inode, the list inode->i_mmap, for shm areas,
 * the list of attaches, otherwise unused.
 */
struct vm_area_struct *vm_next_share;
struct vm_area_struct **vm_prev_share;

struct vm_operations_struct * vm_ops;
unsigned long vm_pgoff; /* offset in PAGE_SIZE units, *not* PAGE_CACHE_SIZE */
struct file * vm_file;
void * vm_private_data; /* was vm_pte (shared mem) */
};

/*
 * vm_flags..
 */
#define VM_READ			0x00000001	/* currently active flags */
#define VM_WRITE			0x00000002
#define VM_EXEC			0x00000004
#define VM_SHARED			0x00000008

#define VM_MAYREAD			0x00000010	/* limits for mprotect() etc */
#define VM_MAYWRITE			0x00000020
#define VM_MAYEXEC			0x00000040
#define VM_MAYSHARE			0x00000080

#define VM_GROWSDOWN		0x00000100	/* general info on the segment */
#define VM_GROWSUP			0x00000200
#define VM_SHM			0x00000400	/* shared memory area, don't swap out */
#define VM_DENYWRITE		0x00000800	/* EXTBSY on write attempts. */

#define VM_EXECUTABLE		0x00001000	
#define VM_LOCKED			0x00002000
#define VM_IO				0x00004000	/* Memory mapped I/O or similar */

#define VM_STACK_FLAGS	0x00000177

/*
 * mapping from the currently active vm_flags protection bits (the
 * low four bits) to a page protection mask..
 */
extern pgprot_t protection_map[16];

/*
 * These are the virtual MM functions - opening of an area, closing and
 * unmapping it (needed to keep files on disk up-to-date etc), pointer
 * to the functions called when a no-page or a wp-page exception occurs.
 */
struct vm_operations_struct {
 void (*open)(struct vm_area_struct * area);
 void (*close)(struct vm_area_struct * area);
 void (*unmap)(struct vm_area_struct *area, unsigned long, size_t);
    void (*protect)(struct vm_area_struct *area, unsigned long, size_t, unsigned int newprot);
    int (*sync)(struct vm_area_struct *area, unsigned long, size_t, unsigned int flags);
    void (*advise)(struct vm_area_struct *area, unsigned long, size_t, unsigned int advise);
    struct page * (*nopage)(struct vm_area_struct * area, unsigned long address, int write_access);
    struct page * (*wp_page)(struct vm_area_struct * area, unsigned long address,
                struct page * page);
    int (*swapout)(struct page *, struct file *);
};

/*
 * A swap entry has to fit into a "unsigned long", as
 * the entry is hidden in the "index" field of the
 * swapper address space.
 */
typedef struct {
    unsigned long val;
} swp_entry_t;

/*
 * Try to keep the most commonly accessed fields in single cache lines
 * here (16 bytes or greater). This ordering should be particularly
 * beneficial on 32-bit processors.
 *
 * The first line is data used in page cache lookup, the second line
 * is used for linear searches (eg. clock algorithm scans).
 */
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
#define get_page(p)         atomic_inc(&(p)->count)
#define put_page(p)         __free_page(p)
#define put_page_testzero(p)        atomic_dec_and_test(&(p)->count)
#define page_count(p)       atomic_read(&(p)->count)
#define set_page_count(p,v)         atomic_set(&(p)->count, v)

/* Page flag bit values */
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

/* Make it prettier to test the above... */
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

/*
 * Error return values for the *nopage functions
 */
#define NOPAGE_SIGBUS (NULL)
#define NOPAGE_OOM ((struct page *) (-1))

/*
 * Various page->flags bits:
 *
 * PG_reserved is set for a page which must never be accessed (which
 may not even be present).
 *
 * PG_DMA has been removed, page->zone now tells exactly whether the
 page is suited to do DMAing into.
 *
 * Multiple processes may "see" the same page. E.g. for untouched
 * mappings of /dev/null, all processes see the same page full of
 * zeroes, and text pages of executables and shared libraries have
 * only one copy in memory, at most, normally.
 *
 * For the non-reserved pages, page->count denotes a reference count.
 * page->count == 0 means the page is free.
 * page->count == 1 means the page is used for exactly one purpose
 * (e.g. a private data page of one process).
 *
 * A page may be used for kmalloc() or anyone else who does a
 * _get_free_page(). In this case the page->count is at least 1, and
 * all other fields are unused but should be 0 or NULL. The
 * management of this page is the responsibility of the one who uses
 * it.
 *
 * The other pages (we may call them "process pages") are completely
 * managed by the Linux memory manager: I/O, buffers, swapping etc.
 * The following discussion applies only to them.
 *
 * A page may belong to an inode's memory mapping. In this case,
 * page->inode is the pointer to the inode, and page->offset is the
 * file offset of the page (not necessarily a multiple of PAGE_SIZE).
 *
 * A page may have buffers allocated to it. In this case,
 * page->buffers is a circular list of these buffer heads. Else,
 * page->buffers == NULL.
 *
 * For pages belonging to inodes, the page->count is the number of
 * attaches, plus 1 if buffers are allocated to the page.
 *
 * All pages belonging to an inode make up a doubly linked list
 * inode->i_pages, using the fields page->next and page->prev. (These
 * fields are also used for freelist management when page->count==0.)
 * There is also a hash table mapping (inode,offset) to the page
 * in memory if present. The lists for this hash table use the fields
 * page->next_hash and page->pprev_hash.
 */

