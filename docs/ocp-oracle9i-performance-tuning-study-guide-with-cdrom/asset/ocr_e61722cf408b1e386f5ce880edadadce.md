init.ora, they should be grouped together and commented appropriately. The init.ora entries will look like this:

```
EVENT='10046 trace name context forever, level 12'
```

The double quotes are part of the actual syntax of this parameter; Notice that each event entry is made up of two components:

+   * The event to be traced, designated by a number (10046 in the example above)
+   * The level to which tracing will be performed, designated by a number (12 in the example above)

The numeric values for both the events and their associated levels are not widely documented. In most cases, Oracle Worldwide Support personnel will provide you with these values when the need for using trace events arises. Setting them to the proper values is important for the event tracing to work properly.

# ## User Trace Files

User trace files are found in the directory specified by the init.ora parameter USER_DUMP_DEST. On systems that follow the OFA model, this directory will be $ORACLE_BASE/SID/admin/$SID/udump on Unix systems and %ORACLE_BASE%\admin\SID\udump on Windows 2000 systems, where *SID* is the name of the Oracle instance that generated the file. User process trace files incorporate the OS process identifier in the trace file name. On Unix systems, they also incorporate the name of the instance that the user was connected to when they were generated. Examples of Unix and Windows 2000 background trace file names are shown here:

+   * Unix System: ora_prod_4327.trc
+   * Windows 2000 System: ora00117.trc

A query can be performed against the V$PROCESS and V$SESSION dynamic performance views in order to identify which user generated a particular trace file. The following code demonstrates how to match a user trace file to the user session that generated it.

```
SQL> SELECT s.username, p.spid
2 FROM v$session s, v$process p
```