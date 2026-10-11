to kill the blocking session. This command disconnects the blocking user’s session and rolls back any uncommitted transactions they had open. Before you can kill a blocking user’s session, you must identify the SID and SERIAL# for their session using V$SESSION. The following example shows how to use DBA_BLOCKERS and V$SESSION to determine the SID and SERIAL# of a blocking user:

```
SQL> SELECT s.username, s.sid, s.serial#\n 2  FROM dba_blockers db, v$session s\n 3  WHERE db.holding_session = s.sid;
```

USERNAME    SID SERIAL#\n----------   --- ------\nJOE           12  8881

> TIP\nIf all users connect to the application using the same Oracle username, try adding the V$SESSION columns OSUSER, MACHINE, or PROGRAM to your query to help identify which user’s session you should kill.

# ## Oracle Objective

### Resolve contention in an emergency

Once you have identified the SID and SERIAL# for the session to be killed, you can issue the ALTER SYSTEM command to actually kill the session:

```
SQL> ALTER SYSTEM KILL SESSION '12,8881';
```

> NOTE\nThe user whose session was killed does not get an immediate indication that this has occurred unless the user is accessing the database at that moment. If they are idle when their session is killed, they will not receive the ORA-00028 “Your Session Has Been Killed” error message until they initiate new activity against the database.

Another technique to reduce locking issues is to use the Oracle9i SQL command ALTER SYSTEM QUIESCE RESTRICTED. If Resource Manager is enabled, issuing this command will cause all inactive user sessions to release their database resources, including locks.