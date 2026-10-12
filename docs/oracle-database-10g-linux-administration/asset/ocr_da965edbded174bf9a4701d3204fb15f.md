| Parameter | Description |
| --- | --- |
| LARGE_POOL_SIZE | The size of the large pool. This is used for shared session memory, parallel execution memory, and disk I/O buffers. |
| LOG_BUFFER | The size of the redo log buffer. The redo log buffer is used for caching redo entries until the log writer process can write them out. |
| PGA_AGGREGATE_TARGET | This specifies the target size for PGA memory and thus makes SORT_AREA_SIZE and HASH_AREA_SIZE obsolete. |
| SESSION_CACHED_CURSORS | This parameter specifies the number of session cursors that can be cached in memory. |
| SHARED_POOL_SIZE | The size of the shared pool. The shared pool contains the library cache and the data dictionary. |

These parameters will affect how the system performs based on a particular workload. Parameters such as the DB_CACHE_SIZE will help some applications perform better, and with other applications it will not much all at all. This chapter is not about performance tuning, but about sizing.

These parameters directly affect the size of the system that you must configure. When the value of these parameters are increased, more system resources are consumed, thus it is necessary to properly size both the parameters as well as the system. Setting parameters too high can often be worse than setting them too low. This is especially true where memory is involved. If Oracle tries to use more than the available physical memory, swapping will occur, thus adversely affecting system performance. In addition, if some parameters are set too high, the Oracle instance might even fail to start.

In Chapter 2, the Oracle architecture was presented to you. Within the Oracle architecture there are two main areas of memory usage: the SGA and the PGA. The SGA memory allocation is determined by many of the Oracle initialization parameters such as DB_CACHE_SIZE, SHARED_POOL_SIZE and LOG_BUFFER, as well as a number of other parameters. With 9i and above the SGA can grow from the startup size, determined by DBA_CACHE_SIZE, etc., up to MAX_SGA_SIZE if this is set, and it is important to make sure that this is the value used for sizing, since it can push a non-paging system to start paging.

In addition to the SGA, there is memory used by each individual process, including the shared server processes and parallel query processes. This memory is variable, based on how much memory is needed at any time. This is the primary area where you can run into problems. It is because of this that Oracle has changed the way PGA memory is allocated.

In the past, you would set parameters such as SORT_AREA_SIZE and HASH_AREA_SIZE, which would define the maximum amount of memory that each individual user process could use. Depending on how much memory each process needed and how many processes there were, this memory could vary and sometimes become quite large.

With Oracle9i, a new parameter was introduced. PGA_AGGREGATE_TARGET sets the optimal amount of memory for all user processes to use. When more processes