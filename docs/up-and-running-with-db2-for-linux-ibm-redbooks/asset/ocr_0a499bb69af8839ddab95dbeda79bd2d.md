# Example 5-31 Sample table preparation for LOAD testing

```
db2inst1@UDBLNX08:"/its0> db2 create table loadtab like employee
DB20001I The SQL command completed successfully.
db2inst1@UDBLNX08:"/its0> db2 "create unique index u_lt_empno on loadtab(empno)"
DB20001I The SQL command completed successfully.
db2inst1@UDBLNX08:"/its0> db2 "export to empl.del of del select * from employee"
SQL3104N The Export utility is beginning to export data to file "empl.del".
SQL3105N The Export utility has finished exporting "32" rows.
Number of rows exported: 32
```

In the following sample, we will use two methods to load data into the LOADTAB, using external source file and using CURSOR answer set as the source for loading separately.

# Example 5-32 Load data from source DEL file into a partitioned table

```
db2inst1@UDBLNX08:"/its0> db2 "load from empl.del of del insert into loadtab"
Agent Type   Node   SQL Code   Result
```

| Agent | Type | Node | SQL Code | Result |
|---|---|---|---|---|
| LOAD |  | 000 | +00000000 | Success. |
| LOAD |  | 001 | +00000000 | Success. |
| LOAD |  | 002 | +00000000 | Success. |
| PARTITION |  | 001 | +00000000 | Success. |
| PRE_PARTITION |  | 000 | +00000000 | Success. |
| RESULTS: | 3 of 3 LOADs completed successfully. |  |  |  |

Summary of Partitioning Agents:
Rows Read          = 32
Rows Rejected      = 0
Rows Partitioned   = 32

Summary of LOAD Agents:
Number of rows read        = 32
Number of rows skipped     = 0
Number of rows loaded      = 32
Number of rows rejected    = 0
Number of rows deleted     = 0
Number of rows committed   = 32

```
db2inst1@UDBLNX08:"/its0> db2 "select dbpartitionnum(empno),count(*) from loadtab group by dbpartitionnum(empno)"
```