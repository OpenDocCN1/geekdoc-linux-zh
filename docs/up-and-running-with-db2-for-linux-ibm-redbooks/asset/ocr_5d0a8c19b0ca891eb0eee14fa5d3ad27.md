+   1. Select a source of SQL statements.
+   2. Click the check box beside the statements that you want to import.
+   3. Click OK.

Source of SQL statements Explained SQL statements

Import SQL statement Check All Uncheck All OK Cancel Apply Help

# Figure 7-5 Importing explained SQL statements to define a workload

The next step is to specify which tables need to collect statistics. As mentioned in the previous paragraph, the advising engine uses workload information in conjunction with the database information such as statistics to recommend indexes. Therefore, if up-to-date statistics for the involved tables don't exist, you need to collect them first to make the recommended indexes usable. Figure 7-6 shows that some tables are chosen for statistics updating.

Updating catalog statistics... In order to provide the best recommendations, the table statistics in your database catalog must be current. If you want to update the table statistics, select the tables required by the specified workload. Updating the table statistics will increase the calculation time. Available Table Selected Table DB2INST1 EMPLOYEE SALES Back Next Finish Cancel

# Figure 7-6 Updating catalog statistics for Design Advisor

Then you can specify the default table space and combined maximum disk space for the recommended objects in Disk Usage window. You can specify when the