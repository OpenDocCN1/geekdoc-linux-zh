is calculated. Including these direct reads in the Buffer Cache hit ratio
calculation would also result in an artificially low hit ratio.

**Session Logical Reads** This statistic indicates the number of times a
request for a data block was satisfied by using a buffer that was already
cached in the Database Buffer cache. For read consistency, some of these
buffers may have contained data from rollback segments.

Figure 5.2 shows how to use these statistics to calculate the hit ratio for the
Database Buffer Cache.

# FIGURE 5.2 Calculating the Database Buffer Cache hit ratio using V$SYSSTAT

```
SQL> SELECT 1 - ((physical.value - direct.value - lobs.value) / logical.value) "Buffer Cache Hit Ratio"
2  FROM v$sysstat physical,
3  v$sysstat direct,
4  v$sysstat lobs,
5  v$sysstat logical
6  WHERE physical.name = 'physical reads'
7  AND direct.name = 'physical reads direct'
8  AND lobs.name = 'physical reads direct (LOB)'
9  AND logical.name = 'session logical reads';
Buffer Cache Hit Ratio
.937164521
```

The results from the query in Figure 5.2 indicate that 93.7 percent of
the time, application users found that the data they were requesting was
already cached in the Buffer Cache. The general formula used in Figure 5.2
to calculate the Database Buffer Cache is:

1 – ((Physical Reads – Physical Reads Direct – Physical Reads Direct [LOB]) ÷ Session Logical Reads)

> According to Oracle, a well-tuned OLTP system should have Database Buffer
> Cache hit ratios of 90 percent or higher.

# Monitoring the Buffer Cache Using STATSPACK

The output from the STATSPACK utility also contains a calculation for the
Database Buffer Cache hit ratio. Figure 5.3 shows the appropriate section
from sample STATSPACK output with the Buffer Cache hit ratio highlighted
in bold.

The results from the sample output show that 92.21 percent of the time,
application users found that the data they were requesting was already
cached in the Buffer Cache.