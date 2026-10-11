Non-zero or steadily increasing values for the statistic REQUEST_FAILURES indicate that the reserved area is too small.

Oracle recommends that you aim to have REQUEST_MISSES and REQUEST_FAILURES near zero in V$SHARED_POOL_RESERVED when using the Shared Pool Reserved Area.

Another way to manage Library Cache space requests by large PL/SQL objects is through the use of the ABORTED_REQUEST_THRESHOLD procedure in the DBMS_SHARED_POOL package. This procedure is used to specify how much of the Library Cache’s memory can be flushed from the Shared Pool’s LRU list when a large PL/SQL object is trying to find space for itself in memory:

```
SQL> EXECUTE dbms_shared_pool.aborted_request_threshold (10000);
```

This example allows a large PL/SQL object to flush up to 10,000 bytes from the Shared Pool’s LRU list. The ABORTED_REQUEST_THRESHOLD limit is specified in bytes as a value between 5,000 and 2,000,000,000. If an application user exceeds this imposed limit, Oracle will return an out of memory error to the user.

# ## Keep Important PL/SQL Code in Memory

Applications that make heavy use of PL/SQL packages and triggers or Oracle sequences can improve their Shared Pool hit ratios by permanently caching these frequently used PL/SQL objects in memory until the instance is shut-down. This process is known as *pinning* and is accomplished by using the Oracle-supplied PL/SQL package DBMS_SHARED_POOL. Pinned packages are stored in the space set aside for this purpose by the `init.ora` parameter SHARED_POOL_RESERVED_SIZE.

Even the command ALTER SYSTEM FLUSH SHARED_POOL does not flush pinned objects. However, pinned objects will be removed from memory at the next instance shutdown.

# **Oracle Objective**

Size and pin objects in the Shared Pool