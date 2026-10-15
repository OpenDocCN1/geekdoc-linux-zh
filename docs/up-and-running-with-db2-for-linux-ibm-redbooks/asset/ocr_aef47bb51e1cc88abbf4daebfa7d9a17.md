+   2. Click the Tables folder. Any existing tables are displayed in the pane on the right side of the window (the contents pane).
+   3. Right-click the table you want in the contents pane, and select Import from the pop-up menu. The Import notebook opens.

Figure 5-19 is a sample for using IMPORT within DB2 Control Center.

![](bbox=[0.28, 0.24, 0.82, 0.72])

Figure 5-19 Using IMPORT within DB2 Control Center

In a partitioned database environment, the import utility can be enabled to use buffered inserts. This reduces the messaging that occurs when data is imported, resulting in better performance. However, since details about a failed buffered insert are not returned, this option should only be enabled if you are not concerned about error reporting.

Use the DB2 bind utility to request buffered inserts capability. The import package, db2uimpm.bnd, must be rebound against the database using the INSERT BUF option. See Example 5-30.

# Example 5-30 Enable INSERT BUF for IMPORT in a partitioned database

```
db2inst1@DBLNX08:~> db2 connect to sample
db2inst1@DBLNX08:~> db2 bind $HOME/sqllib/bnd/db2uimpm.bnd insert buf
```