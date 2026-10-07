![](bbox=[0.165, 0.098, 0.841, 0.532])

**Figure 15.1** The Old-Style Buffer Cache

Typically, the old buffer cache is sized statically by a kernel configuration parameter. Changing the size of the buffer cache requires a kernel rebuild and a reboot.

# ### 15.1.1 Solaris Page Cache

Solaris has a new method, the page cache, of caching file data. The page cache was developed at Sun as part of the virtual memory rewrite in SunOS 4 in 1985 and is used by System V Release 4 Unix. Page cache derivatives are now also used in Linux and Windows NT. The page cache has two major differences from the old caching method. First, it is dynamically sized and can use all memory that is not being used by applications. Second, it caches files rather than disk blocks. The key difference is that the page cache is a virtual file cache rather than a physical block cache. A virtual file cache allows the operating system to retrieve file data by simply looking up the file reference and seek offset. The old way, the operating system invoked the file system, which looked up the physical disk block number corresponding to the file and retrieved that block from the physical block cache. The virtual file cache is far more efficient.