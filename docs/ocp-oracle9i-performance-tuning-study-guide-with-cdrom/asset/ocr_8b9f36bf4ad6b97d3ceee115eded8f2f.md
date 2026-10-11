Sample REPORT.TXT output showing these statistics can be seen in Figures 5.7 and 5.8.

# FIGURE 5.7 REPORT.TXT output showing Free Buffer Inspected statistics

```
SQL> select nl_name 'Statistic',
         nl_change 'Total',
         round(nl_change/(trans_change+2) "Per Transaction",    
         round(nl_change/(start_users + end_users)/2),2) "Per Logon",
         round(nl_change/to_number(to_char(end_time, 'J'))*60*60*24
               - to_number(to_char(start_time, 'J'))*60*60*24 -
               to_number(to_char(end_time, 'SSSSSS'))
               + to_number(to_char(start_time, 'SSSSSS'))
               , 2) "Per Second"
         from
           stats$stats nl,
           stats$stats trans,
           stats$dates
         where
           trans.name='user commits'
           and nl.change != 0
         order by nl.name;
```

|  |  | Total Per Transact | Per Logon | Per Second |
| --- | --- | --- | --- | --- |
| <cmp> |  |  |  |  |
| enqueue timeouts | 5 | .05 | .63 | .02 |
| enqueue waits | 9 | .08 | 1.13 | .04 |
| execute count | 80502 | 745.39 | 10062.75 | 387.05 |
| free buffer inspected | 10 | .25 | 1.45 | .13 |
| free buffer requested | 17415 | 161.25 | 2176.88 | 83.73 |
| immediate (CR) block cleano | 427 | 3.95 | 52.38 | 2.05 |

# FIGURE 5.8 REPORT.TXT output showing Buffer Busy Wait statistics

```
SQL> Rem System wide events for non-background processes (EMON,
SQL> Rem EMON, etc). Tases are in hundredths of seconds. Each one of
SQL> Rem these is a context switch which costs CPU time. By looking at
SQL> Rem the Total Time you can often determine what is the bottleneck
SQL> Rem that processes are waiting for. This shows the total time spent
SQL> Rem waiting for a specific event and the average time per wait on
SQL> Rem that event.
SQL> select nl_event "Event Name",
         nl.event_count "Count",
         nl.time_waited "Total time",
         round(nl.time_waited/nl.event_count, 2) "Avg Time"
         from stats$event nl
         where nl.event_count > 0
         order by nl.time_waited desc;
```

|  |  | Count | Total Time | Avg Time |
| --- | --- | --- | --- | --- |
| SQL*Net message from client | 40057 | 35572 | .89 |
| enqueues | 21 | 4724 | 224.95 |
| library cache load lock | 18 | 3487 | 193.72 |
| log file switch completion | 39 | 2672 | 68.51 |
| db file sequential read | 290 | 2024 | 6.98 |
| dbname ipc reqply | 29 | 1476 | 50.9 |
| log file sync | 98 | 1101 | 11.23 |
| db file scattered read | 450 | 1059 | 2.35 |
| log buffer space | 162 | 1011 | 6.24 |
| switch logfile command | 5 | 651 | 130.2 |
| buffer busy waits | 170 | 246 | 1.45 |
| control file sequential read | 56 | 244 | 4.36 |
| latch free | 119 | 195 | 1.64 |