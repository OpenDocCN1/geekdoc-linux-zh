# Make It Bigger

The simplest way to improve the performance of the Library and Data Dictionary Caches is to increase the size of the Shared Pool. Because the Oracle Server dynamically manages the relative sizes of the Library and Data Dictionary Caches from amongst the total space available to the Shared Pool, making the Shared Pool larger lessens the likelihood that cached information will be moved out of either cache by the LRU mechanism. This has the effect of improving both the Library Cache and Data Dictionary Cache hit ratios.

It is rare to see a situation where the Library Cache’s hit ratios are good, but the Data Dictionary Cache’s are bad, or vice versa. The hit ratios for both of these caches tend to move together as a result of this dynamic allocation of space between the two caches.

The size of the Shared Pool is determined by the init.ora parameter SHARED_POOL_SIZE. This parameter is specified in bytes and by default is set to 64MB on 64-bit operating systems and 16MB on 32-bit operating systems. The current size of the Shared Pool can be determined by querying the V$SGASTAT dynamic performance view:

```
SQL> SELECT pool, sum(bytes) "SIZE"
2    FROM v$sgastat
3    WHERE pool = 'shared pool'
4    GROUP BY pool;
```

POOL                 SIZE
---------- ----------
shared pool 209715200

If you are using Oracle’s Java capabilities, it is important to make sure the Shared Pool is at least 50MB in size. Over 4,000 Java classes are loaded at instance startup, and they require at least this much Shared Pool space to function properly. By default, Oracle9i configures a third pool, the Java Pool, of size 20,000 bytes. The size of the Java Pool is specified by the init.ora parameter JAVA_POOL_SIZE. This pool is used to cache Java state and runtime execution information.