
## Tip: The meaning of ELEAF and NDEL:

- **ELEAF: Number of pseudo empty index leaf pages (NUM_EMPTY_LEAFS)**
  A pseudo empty index leaf page is a page on which all the RIDs are marked as deleted, but have not been physically removed.
- **NDEL: Number of pseudo deleted RIDs (NUMRIDS_DELETED)**
  A pseudo deleted RID is a RID that is marked for deletion. This statistic reports pseudo deleted RIDs on leaf pages that are not pseudo empty. It does not include RIDs marked as deleted on leaf pages where all the RIDs are marked deleted.

```
db2inst1@UDBLNX08:~/test> db2 "reorg indexes all for table emp allow write access cleanup only all on all dbpartitionnums"
DB20001 The REORG command completed successfully.
db2inst1@UDBLNX08:~/test> db2 "reorgchk update statistics on table db2inst1.emp"
Doing RUNSTATS ...
Table statistics:
...
Index statistics:
SCHEMA NAME CARD LEAF ELEAF LVLS ISIZE NDEL KEYS F4 F5 F6 F7 F8 REORG
Table: DB2INST1.EMP
DB2INST1 U_EMP_ENO 49701 201 0 2 6 0 49701 100 90 0 0 0 -----
```

## Figure 5-14 REORG INDEXES and REORGCCHK to update statistics

Then we find that ELEAF and NDEL goes back to 0 as the pseudo deleted pages are physically removed.

Now we reorganize the table as recommended. In the first example (Example 5-21) we use classic table reorganization method with ALLOW READ ACCESS option.

## Example 5-21 REORG TABLE with ALLOW READ ACCESS option

```
db2inst1@UDBLNX08:~/test> db2 "reorg table emp index u_emp_eno allow read access on all dbpartitionnums"
DB20001 The REORG command completed successfully.
```

Then we use the in-place table reorganization method with ALLOW WRITE ACCESS option. Before issuing the command of REORG TABLE, to observe the process of REORG TABLE, you can open another window and keep "GET SNAPSHOT" command running with specified interval. The length of interval depends on the data volume you are operating against and your system's capability. You can do it with a shell script or manually. In our example (Example 5-22), a shell script named "run" is used to run the "GET SNAPSHOT" command at an interval of 2 seconds.

## Example 5-22 Start a monitor program to observe table reorganization procedure

```
db2inst1@UDBLNX08:"/test> run
Usage: run <command_name> [ <sleeping_interval> [ < result_file > ] ]
db2inst1@UDBLNX08:"/test> run "db2 get snapshot for tables on sample" 2
snap_reorgtab_write.out
Program name: "db2 get snapshot for tables on sample"
This program will keep running every 2 seconds for ever,
pls interrupt it with Ctrl+C if needed ...

Command "db2 get snapshot for tables on sample" is running NOW ...
Note: The output of "get snapshot" is gathered into the file "snap_reorgtab_write.out".
```

Follow the startup of monitor program, now we can start in-place table reorganization by using the command shown in Example 5-23.

## Example 5-23 REORG TABLE with INPLACE and ALLOW WRITE ACCESS mode

```
db2inst1@UDBLNX08:"/test> db2 "reorg table emp index u_emp_eno inplace allow write access on all dbpartitionnums"
DB20001I The REORG command completed successfully.
DB21024I This command is asynchronous and may not be effective immediately.
```

From the output you can find that the in-place table reorganization is asynchronous and may not be effective immediately. To determine if the in-place table reorganization is finished or what the current status is, you can use GET SNAPSHOT FOR TABLES ON SAMPLE (here the SAMPLE database is used in our example) to obtain the detailed information for the reorganization. Example 5-24 is the output collected by the monitor program which was started prior to REORG TABLE. The output contains table reorganization information, such as Reorg Type, Start Time, and Status (Started, Truncate, ..., Completed) and so forth.

## Example 5-24 The snapshot information for table reorganization

```
Table Snapshot

First database connect timestamp = 10-17-2002 13:46:35.708637
Last reset timestamp = 
Snapshot timestamp = 10-17-2002 14:54:53.136558
Database name = SAMPLE
Database path = 
/db2home/db2inst1/db2inst1/NODE0000/SQL00001/
```
