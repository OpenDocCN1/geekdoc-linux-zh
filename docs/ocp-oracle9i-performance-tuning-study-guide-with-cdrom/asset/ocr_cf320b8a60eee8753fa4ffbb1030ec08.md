13. B.  If an object that is referenced by a cached SQL statement is altered or dropped, all cached statements that refer to this object will be marked as invalid and will require a re-parse at the next execution of the statement.

14. A.  Invalidationsof SQL that is cached in the shared pool occur when code is recompiled or changes are made on dependent objects, such as adding a column to a table or modifying a view.

15. C.  The V$ROWCACHE view contains two columns, GETMISSES and GETS, that can be used to calculate the hit ratio for the Data Dictionary Cache.

16. A.  A well-tuned OLTP system will have a hit ratio of 85 percent or higher.

17. D.  Pinned objects are not flushed from the shared pool even when the alter system flush shared pool command is issued. To remove these objects, you can use the DBMS_SHARED_POOL.UNKEEP procedure.

18. D.  Improved Shared Pool hit ratios will be achieved if literal values in application SQL are replaced with bind variables because the number of cache hits will increase.

19. C.  The KEEP and UNKEEP procedures of the DBMS_SHARED_POOL package can be used to pin and unpin PL/SQL packages in the Shared Pool.

20. D.  The statistics for FREE_SPACE, REQUEST_MISSES, and REQUEST_FAILURES found in the V$SHARED_POOL_RESERVED view can all be used to determine if the Shared Pool Reserved Area is sized appropriately.

21. B.  The Performance Manager component of the OEM Diagnostics Pack contains several tools that can monitor Library and Dictionary Cache hit ratios.