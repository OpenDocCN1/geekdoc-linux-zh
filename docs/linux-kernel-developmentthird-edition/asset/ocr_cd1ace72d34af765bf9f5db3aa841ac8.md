involved in each, starting with a page read operation. First, the Linux kernel attempts to find the request data in the page cache. The find_get_page() method is used to perform this check; it is passed an address_space and page offset. These values search the page cache for the desired data:

```
page = find_get_page(mapping, index);
```

Here, mapping is the given address_space and index is the desired offset into the file, in pages. (Yes, calling the address_space structure mapping just furthers the naming confusion. I’m replicating the kernel’s naming for consistency, but I do not condone it.) If the page does not exist in the cache, find_get_page() returns NULL and a new page is allocated and added to the page cache:

```
struct page *page;
int error;
```

```
/* allocate the page ... */
page = page_cache_alloc_cold(mapping);
if (!page)
    /* error allocating memory */
```

```
/* ... and then add it to the page cache */
error = add_to_page_cache_lru(page, mapping, index, GFP_KERNEL);
if (error)
    /* error adding page to page cache */
```

Finally, the requested data can be read from disk, added to the page cache, and returned to the user:

```
error = mapping->a_ops->readpage(file, page);
```

Write operations are a bit different. For file mappings, whenever a page is modified, the VM simply calls

```
SetPageDirty(page);
```

The kernel later writes the page out via the writepage() method. Write operations on specific files are more complicated. The generic write path in mm/filemap.c performs the following steps:

```
page = __grab_cache_page(mapping, index, &cached_page, &lru_vec);
status = a_ops->prepare_write(file, page, offset, offset+bytes);
page_fault = filemap_copy_from_user(page, offset, buf, bytes);
status = a_ops->commit_write(file, page, offset, offset+bytes);
```

First, the page cache is searched for the desired page. If it is not in the cache, an entry is allocated and added. Next, the kernel sets up the write request and the data is copied from user-space into a kernel buffer. Finally, the data is written to disk.

Because the previous steps are performed during all page I/O operations, all page I/O is guaranteed to go through the page cache. Consequently, the kernel attempts to satisfy