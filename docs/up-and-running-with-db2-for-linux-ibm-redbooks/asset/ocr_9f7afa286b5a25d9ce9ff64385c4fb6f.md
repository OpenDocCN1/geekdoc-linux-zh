Number of rows exported: 100000

The data across all the three partitions has been exported. If you want to export data for only one partition, for example, data residing on current database partition, you can do it as in Example 5-27.

# Example 5-27 Export data for current partition from sample table "EMP"

```
db2inst1@UD8LNX08:"/its0/datmov> db2 "export to empart0.del of del messages exppart0.msg select * from emp where dbpartitionnum(eno) = current dbpartitionnum"
```

Number of rows exported: 33269

If you want to export data in parallel across different partitions, you can use db2_all or db2batch. For more details regarding the use of db2batch to export data in parallel, refer to IBM DB2 UDB Data Movement Utilities Guide and Reference V8, SC09-4830.

You can also use the DB2 Control Center to invoke EXPORT for tables on Linux platforms. Figure 5-18 is provided for your reference. In the Control Center, you can choose the output file format of export under the File Format options; input SQL statement manually or by SQL Assist Wizard under the SELECT statement area. Also under the Messages file you can specify the messages file to be created that will contain the error, warning, and informational messages associated with the EXPORT operation. In addition, if you want to know the command associated with your choices, click Show Command. A pop-up window appears with detailed commands inside. Furthermore, you may use the Schedule function provided by DB2 for Export operations by choosing the Schedule tab on the window.