# FIGURE 8.27 REPORT.TXT showing undo wait statistics

```
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

# FIGURE 8.28 REPORT.TXT showing undo statistics

```
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

# Rollback Segment Extent Contention

Even when there are no waits occurring for access to the rollback segment header blocks, there may still be waits occurring for access to the blocks