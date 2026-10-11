# ## Configuring the Large Pool

To create a Large Pool, set the `init.ora` parameter `LARGE_POOL_SIZE` to the desired size in bytes. By default, this parameter is zero (i.e., no Large Pool exists) unless the `PARALLEL_AUTOMATIC_TUNING` parameter is set to TRUE, in which case the size of the Large Pool is set automatically. Once configured, the Large Pool's memory area can be used to cache data related to:

+   - I/O slave processes for Database Writer (discussed in Chapter 8, “Tuning Disk I/O”)
+   
+   - Backup and restore operations for Recovery Manager
+   
+   - Shared Server session data
+     - Messaging information for the Parallel Query option

When configuring the Large Pool manually, the minimum non-zero value allowed for `LARGE_POOL_SIZE` is 600K. Once configured, the Oracle Server will automatically use the Large Pool to allocate memory to I/O server processes, RMAN, and Shared Server connections. By doing this, the memory allocated to the Shared Pool will not be consumed by these processes, and will instead be available to application users.

# ## Measuring the Performance of the Large Pool

Once you've configured the Large Pool to take advantage of its ability to enhance the performance of the Shared Pool, you should monitor its performance so that you can determine whether it is optimally configured.

| **Oracle Objective** | **Set the Large Pool** |
|---|---|
| | You can use the POOL column in the dynamic performance view V$SGASTAT to track how the space allocated to the Large Pool is being utilized: |

```
```
SQL> SELECT name, bytes
2    FROM v$sgastat
3    WHERE pool = 'large pool';
```
```