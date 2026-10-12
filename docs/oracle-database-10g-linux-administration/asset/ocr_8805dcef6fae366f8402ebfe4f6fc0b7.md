+   Back up the datafiles that constitute that tablespace using OS or third-party utilities.

+   Mark the end of the tablespace backup using the SQL command `ALTER TABLESPACE tname END BACKUP`.

By marking the beginning and end of the backup, Oracle synchronizes the data files so that they will be useful for restoration. This is all that is necessary to perform the online tablespace backup.

![](bbox=[0.05, 0.32, 0.11, 0.38])

> **NOTE**
> 
> *During an online backup (whenever a tablespace has been marked for backup), additional log records are generated. This is because whole blocks, not just deltas, are written for tablespaces in backup mode. The difference between the amount of redo log information generated in backup mode and non-backup mode can be significant. Thus, it is important to complete online backups as quickly as possible.*

It is important that tablespaces not be left in backup mode for a long period of time. If you think that a tablespace might be in backup mode, you can use the following query to determine the backup state of each of the tablespaces and datafiles in your database:

```
```
SET linesize 120;
Set pagesize 200;

ALTER SESSION SET NLS_DATE_FORMAT = 'YYYY-MM-DD HH24:MI:SS';

COL "Status" FORMAT a10;
COL "Change No" FORMAT 9999;
COL "Backup Started" FORMAT a14;
COL "Tablespace Name" FORMAT a20;
COL "Datafile Name" FORMAT a40;

SELECT
  ts.name AS "Tablespace Name"
  , b.status AS "Status"
  , b.change# AS "Change No"
  , b.time AS "Backup Started"
  , df.name AS "Datafile Name"
FROM v$backup b, v$tablespace ts, v$datafile df
WHERE b.file# = df.file#
AND df.ts# = ts.ts#;
```
```