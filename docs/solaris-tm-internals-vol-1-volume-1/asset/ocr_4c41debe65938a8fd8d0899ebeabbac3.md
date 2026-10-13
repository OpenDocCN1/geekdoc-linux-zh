# Table 6-4  *Solaris 7 Resource Map Allocator Functions from `<sys/map.h>`*

| Function | Description |
|---|---|
| `rmallocmap()` | Dynamically allocates a map. Does not sleep.<br>Driver-defined basic locks, read/write locks, and sleep locks can be held across calls to this function.<br>DDI-/DKI-conforming drivers may only use map structures that have been allocated and initialized with `rmallocmap()`. |
| `rmallocmap_wait()` | Dynamically allocates a map. It does sleep.<br>DDI-/DKI-conforming drivers can only use map structures that have been allocated and initialized with `rmallocmap()` and `rmallocmap_wait()`. |
| `rmfreemap()` | Frees a dynamically allocated map. Does not sleep.<br>Driver-defined basic locks, read/write locks, and sleep locks can be held across calls to this function.<br>Before freeing the map, the caller must ensure that nothing is using space managed by the map and that nothing is waiting for space in the map. |
| `rmalloc()` | Allocates *size* units from the given map. Returns the base of the allocated space. In a map, the addresses are increasing and the list is terminated by a 0 size. Algorithm is first-fit. |
| `rmalloc_wait()` | Like `rmalloc`, but waits if necessary until space is available. |
| `rmalloc_locked()` | Like `rmalloc`, but called with lock on map held. |
| `rmfree()` | Frees the previously allocated space at *addr* of *size* units into the specified map.<br>Sorts *addr* into map and combines on one or both ends if possible. |
| `rmget()` | Allocates *size* units from the given map, starting at address *addr*. Returns *addr* if successful, 0 if not. This may cause the creation or destruction of a resource map segment.<br>This routine returns failure status if there is not enough room for a required additional map segment. |

provides functions that implement a page-level memory allocator by using one of those segments—the kernel map segment.