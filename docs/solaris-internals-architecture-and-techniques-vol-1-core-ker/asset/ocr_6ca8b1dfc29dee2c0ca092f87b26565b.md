# Kernel Memory Allocation

The kmastat command shows summary information for each statistic and a system-wide summary at the end. The columns are shown in Table 6-13.

# Table 6-13 kmastat Columns

| Parameter | Description |
|--- | --- |
| Cache name | The name of the cache, as supplied during kmmem_cache_create(). |
| buf_size | The size of each object within the bytes. |
| buf_avail | The number of free objects in the cache. |
| buf_total | The total number of objects in the cache. |
| Memory in use | The amount of physical memory consumed by the cache bytes. |
| Allocations succeeded | The number of allocations succeeded. |
| Allocations failed | The number of allocations that failed. These are likely to be allocations that specified KM_NOSLEEP during memory pressure.

A detailed version of the per-cache statistics is exported by the kstat mechanism. You can use the netstat -k command to display the cache statistics, which are described in Table 6-14.

```
# netstat -k ufs_inode_cache
ufs_inode_cache:
buf_size 440 align 8 chunk_size 440 slab_size 8192 alloc 20248589
alloc_fail 0 20770500 depot_alloc 65734 depot_free 678433
depot_contention 85 global_alloc 602986 global_free 578089
buf_constructed 0 global_alloc 7971 buf_use 24897 buf_total 32868
buf_max 41076 slab_create 2802 destroy 96 memory_class 0
hash_size 0 hash_lookup depot 0 hash_scale 0 full magazines 0
empty_magazines 0 magazine_size 31 alloc_from_cpu0 953811
free_to_cpu0 10344474 buf_avail_cpu0 0 alloc_from_cpu1 9404448
free_to_cpu1 9169504 buf_avail_cpu1 91690
```

# Table 6-14 Slab Allocator Per-Cache Statistics

| Parameter | Description |
|--- | --- |
| buf_size | The size of each object within the cache bytes. |
| align | The alignment boundary for objects within the cache. |
| chunk_size | The allocation unit for the cache bytes. |
| slab_size | The size of each slab within the cache bytes.