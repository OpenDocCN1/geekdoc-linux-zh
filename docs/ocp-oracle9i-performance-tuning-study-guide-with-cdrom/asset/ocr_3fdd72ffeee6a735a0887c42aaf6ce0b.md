cache misses occur when the user does not find the requested data to already be cached in memory—causing the data to be read from disk instead. High cache hit ratios indicate that your application users are frequently finding that the data buffers they need are already in memory. The hit ratio information for the Database Buffer Cache can be found in several places:

+   - V$SYSSTAT

+   - STATSPACK output

+   - UTLBSTAT.SQL/UTLLESTAT.SQL output (REPORT.TXT)

Additionally, there are also non-hit ratio measures of Database Buffer Cache effectiveness, including:

+   - Free Buffer Inspected waits

+   - Buffer Busy Wait events

+   - Free Buffer Wait events

Oracle Enterprise Manager also contains graphical tools that contain useful information about Buffer Cache performance. The following sections discuss each of these measures of Buffer Cache performance.

Oracle Objective

**Monitor the use of the Buffer Cache, also the different pools within the Buffer Cache**

# Monitoring the Buffer Cache Using V$SYSSTAT

The V$SYSSTAT dynamic performance view contains statistics regarding overall system performance, gathered since instance startup. The names of the four columns contained in the V$SYSSTAT view, along with descriptions of their contents, are shown in Table 5.3.

TABLE 5.3 Contents of V$SYSSTAT

Column Name | Description
|STATISTIC# | The identifier associated with the name of the performance statistic.
|NAME | The name of the performance statistic.