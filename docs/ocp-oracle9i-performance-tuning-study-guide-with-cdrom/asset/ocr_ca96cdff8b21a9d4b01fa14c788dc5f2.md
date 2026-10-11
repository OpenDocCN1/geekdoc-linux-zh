# **FIGURE 10.18**  Changing the active resource consumer group for a connected user

```
SQL> EXECUTE dbms_resource_manager.switch_consumer_group_for_user ( user => 'BETTY', consumer_group => 'POWER_USERS');

PL/SQL procedure successfully completed.
```

Any changes made to the active resource plan will take effect immediately.

In some applications, the application connects to the database with the same database username for all users (even though each application user has a unique login name). In these cases, the technique shown in Figure 10.18 cannot be used since all connected users would then have the same RCG activated. In this situation, you can use the `SWITCH_CONSUMER_GROUP_FOR_SESS` procedure in the `DBMS_RESOURCE` package to change the active RCG for an individual user's session---even if that user is connected to the database with the same username as another connected user. This procedure accepts the `SID` and `SERIAL#` of the session you wish to change as input parameters. Both `SID` and `SERIAL#` are identified by querying `V$SESSION`. Figure 10.19 demonstrates how this procedure could be used to change the RCG for just Betty's session when all application users connect to the database using the database username `APPS`.

# **FIGURE 10.19**  Changing the active resource consumer group for a specified session

```
SQL> SELECT sid, serial#, username, consumer
 2   FROM v$session
 3   WHERE username = 'betty';

    SID SERIAL# USERNAME   CONSUMER
---------- ---------- ------------------- ------------------------
       13     14 APPS     betty

1 row selected.

SQL> EXECUTE dbms_resource_manager.switch_consumer_group_for_sess ( session_id => 13, session_serial => 14, consumer_group => 'POWER_USERS');

PL/SQL procedure successfully completed.
```

If they have been granted the privileges allowing them to switch to that particular consumer group, non-DBA users can also change their active resource consumer group by using the `SWITCH_CURRENT_CONSUMER_GROUP` procedure in the `DBMS_SESSION` package.