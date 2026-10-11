When using RAID striping, the value of `DB_FILE_MULTIBLOCK_READ_COUNT` should be set to a multiple of the stripe size.

Another view useful for monitoring full table scan operations is the `V$SESSION_LONGOPS` view. This view shows activity associated with selected long-running operations like snapshot refreshes, recovery operations, and parallel query jobs. Table 8.6 shows selected columns from the `V$SESSION_LONGOPS` view that can be used for monitoring full table scan activity.

# TABLE 8.6  Selected `V$SESSION_LONGOPS` Columns

| Column Name | Description |
|---|---|
| SID | Session identifier of the user session running the long operation |
| SERIAL# | Serial number of the user session running the long operation |
| OPNAME | Name of the long operation being performed (`TABLE SCAN` in the case of full table scans) |
| START_TIME | Time that the long operation started |
| SOFAR | The total units of work completed so far |
| TOTALWORK | The total units of work to be performed |

Figure 8.7 shows a query on `V$SESSION_LONGOPS` that uses these columns.

# FIGURE 8.7  Query on `V$SESSION_LONGOPS`

```
SQL> SELECT username, opname, ROUND(((totalwork-sofar)/totalwork)*4,100) "PCT_REMAINING"
2       FROM v$session_longops
3      WHERE time_remaining > 0;

USERNAME            OPNAME                    PCT_REMAINING
------------        ----------------------    ------------
JOE                 Sort Output               45.00
BRENDA              Table Scan                9.54
EMILY               SQL Execution             11.97
```