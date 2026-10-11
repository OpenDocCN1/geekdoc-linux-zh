```
SQL> ALTER SYSTEM SET db_keep_cache_size=150M;
SQL> ALTER SYSTEM SET db_recycle_cache_size=50M;
```

If the value for SGA_MAX_SIZE is set too low to allow you to dynamically add the two additional Buffer Pools, then you will have to set them manually.

# Manually Creating Buffer Pools

The SGA_MAX_SIZE parameter must be set to a suitably large value to accommodate all the SGA components. If the value is too low, you may not be able to create the Keep and Recycle Pools. You can edit init.ora, and increase the values for SGA_MAX_SIZE, DB_CACHE_SIZE, DB_KEEP_CACHE_SIZE, and DB_RECYCLE_CACHE_SIZE all at one time, before shutting down and restarting the instance for them to take effect. These parameters were described previously in Table 5.4.

Using our desired values of 150MB for the Keep Pool, 50MB for the Recycle Pool, and 300MB for the Default Pool, we might configure our init.ora like this:

```
# Maximum size of the SGA, must be large enough to hold
# the Shared Pool, Buffer Cache, and Redo Log Buffer
SGA_MAX_SIZE = 1G
#
# Desired total size of the Default Buffer Pool
DB_CACHE_SIZE = 300M
#
# Desired total size of the Keep Buffer Pool
DB_KEEP_CACHE_SIZE = 150M
#
# Desired total size of the Recycle Buffer Pool
DB_RECYCLE_CACHE_SIZE = 50M
```

![](bbox=[0.13, 0.72, 0.2, 0.78])

> The Oracle8i init.ora parameters formerly used to create multiple Buffer Pools, DB_BLOCK_BUFFERS, BUFFER_POOL_KEEP, BUFFER_POOL_RECYCLE, and DB_BLOCK_LRU_LATCHES, should no longer be used in Oracle9i as they will be made obsolete in future Oracle releases. Use the new init.ora parameters discussed here instead.

Once the Buffer Pools are created with the appropriate sizes, you can assign the segments to the appropriate pools.