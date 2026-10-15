
In the workload definition window, as Figure 7-4 shows, at first, you need to specify a name for the workload, then you click Add to add a SQL statement into the workload, with SQL statement name and execution frequency specified. Adding multiple SQL statements are also allowed here, you simply need to select Add again to add an additional SQL statement.

![](img/d95c931f4f3da4a6bd0ee55148fefad7_273_0.png)

### Figure 7-4 Defining workload for Design Advisor

You can also choose Import, which is located on the right side of the window to import a workload from explained SQL statements, as Figure 7-5 shows.

- 1. Select a source of SQL statements.
- 2. Click the check box beside the statements that you want to import.
- 3. Click OK.

Source of SQL statements: Explained SQL statements

Import SQL statement: Check All, Uncheck All, OK, Cancel, Apply, Help

### Figure 7-5 Importing explained SQL statements to define a workload

The next step is to specify which tables need to collect statistics. As mentioned in the previous paragraph, the advising engine uses workload information in conjunction with the database information such as statistics to recommend indexes. Therefore, if up-to-date statistics for the involved tables don't exist, you need to collect them first to make the recommended indexes usable. Figure 7-6 shows that some tables are chosen for statistics updating.

Updating catalog statistics...

In order to provide the best recommendations, the table statistics in your database catalog must be current. If you want to update the table statistics, select the tables required by the specified workload. Updating the table statistics will increase the calculation time.

Available Table Selected Table DB2INST1 EMPLOYEE SALES Back Next Finish Cancel

### Figure 7-6 Updating catalog statistics for Design Advisor

Then you can specify the default table space and combined maximum disk space for the recommended objects in Disk Usage window. You can specify when the advisor engine should calculate the recommendations in the Calculate window. If you want to start the calculation at once, choose Now in the window, and then recommendations are given in the Recommendations window, as shown in the Figure 7-7.

Here if you want to change the name for the recommended index instead of using the name given by DB2, you can click the original name shown in the Name field, and then input the name you desire. You can click Show SQL to obtain detailed SQL statements to create the index, and you can also toggle the check box in the Create field to point out whether or not you want to have the index created by DB2.

![](img/d95c931f4f3da4a6bd0ee55148fefad7_275_0.png)

### Figure 7-7 Recommended indexes by Design Advisor

If some indexes for the chosen tables already exist, the Design Advisor can tell you if these indexes remain unused in the specified workload. Then you can specify if you want to drop those unused indexes — make sure that dropping the "unused" indexes won't impact other workloads before you choose to do that.

The remaining step is to schedule the running of recommended SQL statements, including create index and drop index, and then the related indexes will be created or dropped.

You can also run Design Advisor from the command line, if you are familiar with this. Example 7-1 consists of three steps. The first step is to define a workload, the second step is to run statistics for the related tables, and then the third step is to run the db2advis utility from the command line to obtain recommendations. From the output you can see that the timerons for workload running with and without recommended indexes are displayed, and the improvements by using the recommended indexes are also evaluated. In addition, by using the parameter -o, the index creation script of the recommendations can be placed into a file.

### Example 7-1 Using db2advis to recommend index creation for specific workload

```
$ cat sample.sql
--#SETFREQUENCY 100
select count(*) from sales where region = ?;
--#SETFREQUENCY 3
select projno, sum(comm) tot_comm from employee, emp_act
where employee.empno = emp_act.empno and
employee.job='DESIGNER'
group by projno
order by tot_comm desc;
--#SETFREQUENCY 50
select * from sales where sales_date = ?;

$ db2 "runstats on table db2inst1.employee with distribution allow write access"
DB20000I The RUNSTATS command completed successfully.
$ db2 "runstats on table db2inst1.sales with distribution allow write access"
DB20000I The RUNSTATS command completed successfully.
$ db2 "runstats on table db2inst1.emp_act with distribution allow write access"
DB20000I The RUNSTATS command completed successfully.

$ db2advis -d sample -i sample.sql -t 0 -o ad1.sql
execution started at timestamp 2002-11-11-17.33.32.188732
  found [3] SQL statements from the input file
  recommending indexes...
Initial set of proposed indexes is ready.
Found maximum set of [4] recommended indexes
Cost of workload with all indexes included [1.258857] timerons
total disk space needed for initial set [ 0.035] MB
total disk space constrained to          [ -1.000] MB
  4 indexes in current solution
[101.4306] timerons (without indexes)
[ 1.2589] timerons (with current solution)
[%98.76] improvement
```
