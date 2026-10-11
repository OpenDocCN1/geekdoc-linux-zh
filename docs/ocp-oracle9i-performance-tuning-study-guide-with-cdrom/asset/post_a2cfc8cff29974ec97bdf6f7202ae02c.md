
## Oracle Objective

Use the dynamic performance views to check rollback segment performance.

### Measuring Rollback Segment Header Contention

The Oracle Server uses a transaction table stored in the header block of each rollback segment to track the transactions that use the segment to store their before-images. This header block is generally cached in the Database Buffer Cache so that all users can access it when trying to store their transaction before-images. On a busy OLTP system, users may experience a wait for access to these *rollback segment header* blocks, thereby causing their transaction performance to decline.

You can measure the frequency with which these waits are occurring using the V$SYSTEM_EVENT, V$WAITSTAT, and V$ROLLSTAT dynamic performance views as well as the output from STATSPACK and REPORT.TXT.

### Using V$SYSTEM_EVENT to Measure Undo Header Contention

The V$SYSTEM_EVENT view tracks performance related information on rollback segments via the *undo segment tx slot* statistic. The following query shows how to display this information:

```sql
SQL> SELECT event, total_waits,
  2            time_waited, average_wait
  3      FROM v$system_event
  4     WHERE event like '%undo%';
```

| EVENT | TOTAL_WAITS | TIME_WAITED | AVERAGE_WAIT |
|---|---|---|---|
| undo segment tx slot | 28070 | 18 | .000641254 |

This query indicates that the average wait for access to the header blocks of the rollback segments was .0006 100ths seconds, essentially zero.

![](img/832fbc6aca8b6075843ca6f2356c0a8d_469_0.png)

Ideally, the value of the AVERAGE_WAIT statistic should be consistently at or near zero.

### Using V$WAITSTAT to Measure Undo Header Contention

The V$WAITSTAT view contains information on block contention statistics. Included in these statistics are counts for the number of times application users have experienced a wait for access to the header block of rollback segments. The following query shows how this information appears in the V$WAITSTAT view:

```sql
SQL> SELECT class, count
2 FROM v$waitstat
3 WHERE class IN ('undo header',
4 'system undo header')
```

| CLASS | COUNT |
|---|---|
| system undo header | 0 |
| undo header | 12 |

The statistic for *system undo header* relates to the system rollback segment. The *undo header* statistic is for the non-system rollback segments. This query indicates that there was no contention for the system rollback segment's header, but that there were 12 occasions where waits occurred for access to the headers of non-system rollback segments.

![](img/832fbc6aca8b6075843ca6f2356c0a8d_470_1.png)

Ideally, the counts for these waits should be consistently at or near zero.

### Using V$ROLLSTAT to Measure Undo Header Contention

The V$ROLLSTAT view contains detailed information regarding the behavior of the rollback segments in the database. In particular, the columns USN, GETS, and WAITS are particularly useful for measuring contention for the rollback segment's header. Table 8.8 shows the descriptions of each of these columns.

#### Table 8.8 V$ROLLSTAT Columns Used to Measure Header Contention

| **Column** | **Description** |
| :--- | :--- |
| USN | Undo Segment Number, the internal system-generated number assigned to the rollback segment |
| GETS | Number of times a user's Server Process needed to access the rollback segment header and did so successfully |
| WAITS | Number of times a user Server Process needed to access the rollback segment header and experienced a wait |

Using these columns, and joining V$ROLLSTAT to the V$ROLLNAME view on the common column USN, each rollback segment's name can be obtained, allowing you to construct a query that will return the get ratio for each rollback segment header in your database:

```sql
SQL> SELECT n.name, s.usn,
        2     DECODE (s.waits,0,1
        3     ,1-(s.waits/s.gets))
        4     'RBS Header Get Ratio'
        5 FROM v$rollstat s, v$rollname n
        6 WHERE s.usn = n.usn
        7 ORDER BY usn;
```

| NAME | USN | RBS Header Get Ratio |
| :--- | :--- | :--- |
| SYSTEM | 0 | 1 |
| RBS01 | 1 | .97 |
| RBS02 | 2 | 1 |
| RBS03 | 3 | 1 |
| RBS04 | 4 | .8425 |
| RBS05 | 5 | 1 |
| RBSBIG | 6 | 1 |

The output from this query shows that most of the rollback segments are not experiencing any waits for access to their headers. Only RBS01 and RBS04 experienced waits at all.

> Oracle recommends that a well-tuned OLTP system have a rollback segment header get ratio of 95 percent or higher for all rollback segments.

### Using STATSPACK Output to Measure Undo Header Contention

The output from the STATSPACK utility also produces useful information for measuring the rollback segment header contention. Figure 8.26 shows sample output from a STATSPACK report that includes rollback segment performance statistics.

#### FIGURE 8.26 STATSPACK output showing undo statistics

```
Rollback Segment Stats for DB: PROD Instance: prod Snaps: 1 -2
-A high value for "Pct waits" suggests more rollback segments may be required
->RBS stats may not be accurate between begin and end snaps when using Auto undo management, as RBS may be dynamically created and dropped as needed
```

| RBS NO | Trans Table Gets | Pct Waits | Undo Bytes Written | Wraps | Shrinks | Extends |
| --- | --- | --- | --- | --- | --- | --- |
| 0 | 3.0 | 0.00 | 0 | 0 | 0 | 0 |
| 2 | 10.0 | 0.00 | 122 | 0 | 0 | 0 |
| 3 | 13.0 | 0.00 | 0 | 0 | 0 | 0 |
| 4 | 9.0 | 0.00 | 122 | 0 | 0 | 0 |
| 5 | 9.0 | 0.00 | 138 | 0 | 0 | 0 |
| 17 | 46.0 | 0.00 | 106,992 | 21 | 0 | 10 |
| 18 | 4.0 | 0.00 | 1,620 | 4 | 0 | 2 |
| 19 | 15.0 | 0.00 | 138 | 0 | 0 | 0 |

The Pct Waits column in the output in Figure 8.26 shows that no transactions experienced waits while trying to access the rollback segment headers.

### Using REPORT.TXT to Measure Undo Header Contention

Rollback segment header contention statistics are also written to the REPORT.TXT file. Figures 8.27 and 8.28 show the sections from REPORT.TXT, which contain the information of rollback segment header contention.

#### FIGURE 8.27 REPORT.TXT showing undo wait statistics

```sql
SQL> Rem buffer busy wait statistics. If the value for 'buffer busy wait' in
SQL> Rem the wait event statistics is high, then this table will identify
SQL> Rem which class of blocks is having high contention. If there are high
SQL> Rem 'undo_header' waits then add more rollback segments. If there are
SQL> Rem high 'segment_header' waits then adding freelist$ might help, check
SQL> Rem $$session_wait to get the addresses of the actual blocks having
SQL> Rem contention.
SQL> select * from stats$waitstat
      2    where count != 0
      3    order by count desc;

CLASS               COUNT            TIME
---------------------------  -----------  -----------
data block                     164               241
segment header                  3                 0
undo header                     2                 0
undo block                      1                 0
```

#### FIGURE 8.28 REPORT.TXT showing undo statistics

```sql
SQL> set lines 189;
SQL> set numwidth 19;
SQL> Rem Waits_for_trans_tbl high implies you should add rollback segments.
SQL> select * from statsroll;
UNDO_SEGMENT_TRANS_TBL_G  TRANS_TBL_WAITS UNDO_BYTES_WRITTEN SEGMENT_SIZE_BYTES XACTS SHRINKS WRAPS
----------------------  ---------------  ----------------  -------------------  -----  ------  -----
        0             3                     0                401490            0      0      0
        1            122                    0              184064               -1      0      3
        2             494                   0              604680             778240      0     11
        3             363                   0              192400             188416      0      2
        4             223                   0              679460             969312      0     12
        5             436                   0              292592             480560      0      5
        6            1373                   0              8138146            9428992      0     23
        7            1674                   0              8722234           10477568      0     24
        8            1634                   0              9959844           10477568      0     24
        9             271                   0               371298             516096      1      7
       10            1375                   0              6556042            7331840      0     21
```

The output in Figure 8.27 shows that waits for access to non-system rollback segment headers occurred twice between the time UTLBSTAT.SQL and UTLESTAT.SQL were executed.

Because the output in Figure 8.28 shows that the value for TRANS_TBL_WAITS waits were all zero during the monitoring period, this indicates that no contention occurred while trying to access the undo segment headers.

### Rollback Segment Extent Contention

Even when there are no waits occurring for access to the rollback segment header blocks, there may still be waits occurring for access to the blocks
