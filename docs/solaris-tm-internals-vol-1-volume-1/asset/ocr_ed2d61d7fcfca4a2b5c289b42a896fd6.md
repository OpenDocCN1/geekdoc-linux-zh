# Table 5-6  *Anon Layer Functions (Continued) (Continued)*

| Flag | Protection Mode |
|---|---|
| `anon_decref()` | Decrements the reference count of an anon page. If the reference count goes to zero, frees it and its associated page (if any). |
| `anon_dup()` | Duplicates references to size bytes worth of anon pages. Used when duplicating a segment that contains private anon pages. |
| `anon_free()` | Frees a group of size anon pages, size in bytes, and clears the pointers to the anon entries. |
| `anon_get_next_ptr()` | Returns the anon pointer for the first valid entry in the anon list, starting from the given index. |
| `anon_getpage()` | Returns the kept page(s) and protections to the segment driver. |
| `anon_get_ptr()` | Returns the pointer from the list for a specified anon index. |
| `anon_pages()` | Returns a count of the number of existing anon pages in the anon array in the range. |
| `anon_private()` | Turns a reference to an object or shared anon page into a private page with a copy of the data from the original page. |
| `anon_release()` | Frees the array of pointers. |
| `anon_resvmen()` | Reserves anon space. |
| `anon_set_ptr()` | Sets list entry with a given pointer for a specified offset. |
| `anon_unresv()` | Gives back an anon reservation. |
| `anon_zero()` | Allocates a private zero-filled anon page. |
| `anonmap_alloc()` | Allocates and initializes an anon map structure for segment associating the given swap reservation with the new anon map. |
| `anonmap_free()` | Frees an anon map structure. |
| `anonmap_getpages()` | Allocates array of private zero-filled anon pages for empty slots and page slots for nonempty slots within given range. |
| `non_anon()` | Returns true if the array has some empty slots. |
| `set_anoninfo()` | Called from clock handler to sync ani_free value. |

# 5.5.2 The swaps Layer

Each physical page of memory is identified by its vnode and offset. The vnode and offset identify a backing store that tells where to find the page when it’s not in physical memory. For a regular file, the physical page caching the file has a vnode and offset that are simply the file’s vnode and offset. Swap space is used as a back-