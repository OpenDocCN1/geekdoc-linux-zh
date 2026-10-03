![](bbox=[0.07, 0.09, 0.44, 0.38])

Figure 1. Stale Data Problem

![](bbox=[0.07, 0.43, 0.44, 0.73])

Figure 2. Data Destruction by Dirty Cache Lines

# Cache-Line Interference

The situation where two sets of independent data lie in the same cache line, potentially leading to the data destruction detailed above, is termed cache-line interference. If you are laying out data structures in memory, the general rule to avoid this situation is never, ever have data that can be modified outside of the caches mixed with data the CPU may ordinarily use. If you absolutely have to violate this rule, make sure all externally modifiable elements of the structure are aligned L1_CACHE_BYTES, a value set at compile time to the largest possible cache width value for all the processors on which your

code may run. The best thing to do is use kmalloc to allocate two separate regions. kmalloc never allocates two regions that overlap in a cache line.

# Cache Management Instructions

The most basic instruction, called an invalidate, simply ejects the nominated line from all caches. Any reference to data in that line causes it to be re-fetched from main memory. Thus, the stale data problem may be resolved by invalidating the cache line before reading the data. In Linux, such an invalidation is done with:

```
void
dma_cache_inv(unsigned long address
    unsigned long size);
```

where address is the virtual address on which to begin, and size is the length of data to invalidate. Note that size is rounded up automatically to a multiple of the cache line width.

For write back caches, any dirty cache line may be written out, or flushed, to main memory using:

```
void
dma_cache_wback(unsigned long address,
    unsigned long size);
```

This flushing must be done before anything changes the

![](bbox=[0.52, 0.5, 0.92, 0.92])