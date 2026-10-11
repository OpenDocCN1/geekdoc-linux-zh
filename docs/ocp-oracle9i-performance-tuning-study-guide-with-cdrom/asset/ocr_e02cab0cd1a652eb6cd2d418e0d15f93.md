![](bbox=[0.1, 0.1, 0.95, 0.12])

```
SQL> SELECT sw.username "WAITING_USER", bu.username "LOCKING_USER",
2 dw.lock_type, dw.mode_held, dw.mode_requested
3 FROM dba_waiters dw, V$session s, V$session bu
4 WHERE dw.waiting_session = s.sid
5 AND dw.holding_session = bu.sid;
```

| WAITING_USER | LOCKING_USER | LOCK_TYPE | MODE_HELD | MODE_REQUEST |
|:-------------|:-------------|:----------|:----------|:-------------|
| MATT         | JOE          | Transaction | Exclusive | Exclusive     |

The output in Figure 9.7 shows that the user Matt is waiting to obtain an exclusive lock on the same table that user Joe currently has an exclusive transaction lock on.

# Using `DBA_BLOCKERS` to Monitor Lock Contention

Often, the DBA is not concerned with what type of lock other users are trying to obtain; they are only concerned with determining which user is causing the lock contention so that the lock contention can be corrected using one of the techniques described in the next section. The `DBA_BLOCKERS` data dictionary view is the best source of this type of succinct locking information because the `DBA_BLOCKERS` view contains only one column, `HOLDING_SESSION`, which displays the SIDs of the user sessions that are blocking the lock requests of other application users. The following example shows how you can identify the application user that is blocking other users by joining `DBA_BLOCKERS` to `V$SESSION`:

```
SQL> SELECT s.username
2 FROM dba_blockers db, V$session s
3 WHERE db.holding_session = s.sid;
```

| USERNAME |
|:---------|
| JOE      |

This output shows that the user Joe is currently blocking at least one another application user from obtaining a requested lock.

![](bbox=[0.13, 0.82, 0.24, 0.89])

As an alternative to constructing your own queries on the `DBA_BLOCKERS` and `DBA_WAITERS` data dictionary views, you can also use the Oracle-supplied script, `UTLLOCKT.SQL` to display locking information. This script is found in `ORACLE_HOME/rdbms/admin` on Unix systems and `ORACLE_HOME\rdbms\admin` on Windows 2000 systems.