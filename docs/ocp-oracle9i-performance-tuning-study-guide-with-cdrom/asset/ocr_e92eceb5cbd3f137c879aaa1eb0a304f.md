# Collecting Performance Statistics Using STATSPACK

Once the STATSPACK components are configured, you can use them to monitor your database's performance. STATSPACK performance monitoring can be done in two ways:

+   Manually executing the STATSPACK .SNAP procedure
+   Automatically using the SPAUTO.SQL scheduling script

Oracle Objectives  
|  |  |
| Describe how STATSPACK collects statistics | Collect statistics using STATSPACK |

# Collect Statistics Using Manual STATSPACK Execution

To manually initiate the collection of database performance statistics using the STATSPACK utility, you must execute the SNAP procedure in the STATSPACK PL/SQL package by issuing the following command while logged into SQL*Plus as the PERFSTAT user:

```
SQL> execute statspack.snap
```

When the SNAP procedure is executed, a snapshot of the current values for many database performance statistics are captured and stored in the tables that reside in the PERFSTAT schema. These statistics will then be compared to the performance statistics gathered at a later point in time when the STATSPACK .SNAP procedure is executed a second time. However, unlike ULBSTAT.SQL and ULESTAT.SQL discussed in the previous section, the STATSPACK statistics are not deleted after the ending statistics are gathered. Instead, the statistics from a third, fourth, or infinite number of snapshots can be captured and stored indefinitely in the PERFSTAT schema tables. Performance statistics can then be generated between any two points in time when snapshots were taken.

# Collect Statistics Using Automatic STATSPACK Execution

Since the STATSPACK utility has the ability to collect many performance statistic snapshots, you may want to schedule snapshots at regular intervals throughout the day, week, or month. Oracle provides an SQL script just for this purpose. The script, called SPAUTO.SQL, uses Oracle's DBMS\_JOBS package to schedule the snapshot statistic data collection.