
## Logical Standby Database Configuration

As with the configuration of a physical standby database, the logical standby database configuration can be broken into three steps: the preparation stage, the configuration stage and the postconfiguration stage. The prerequisites for a logical standby database are stricter than for a physical standby database.

### Preparation

Before starting logical standby database creation, you should check the prerequisites. In this configuration, some datatypes are not supported. The unsupported datatypes are BFILE, ROWID, UROWID, REFS, varrays, nested tables, XML types, and user-defined data types. If you are using any of these datatypes in your tables, these tables will be skipped by SQL Apply. If you need to, change the datatype on the primary database before you begin configuring the logical standby database. In addition to the skipped data types, there are a number of tables, sequences and views, and DDL statements (including, notably, ALTER DATABASE, ALTER SESSION, and ALTER SYSTEM) that will be skipped as well, including:

- Most schemas that ship with the Oracle database
- Tables with unsupported datatypes
- Tables using table compression

Oracle PL/SQL-supplied packages that modify system metadata typically are not supported by SQL Apply. Examples of such packages include DBMS_JAVA, DBMS_REGISTRY, DBMS_ALERT, DBMS_SPACE_ADMIN, DBMS_REFRESH, DBMS_SCHEDULER, and DBMS_AQ.

To determine if the primary database contains any unsupported objects, query the DBA_LOGSTDBY_UNSUPPORTED view. Unlike the physical standby database, where the ROWIDs of each record in the database are identical, those in the logical standby database might be different. Therefore, you must use a different mechanism to match updated rows on the standby database with rows on the primary database. This could be via either primary keys or unique indexes.

### Deployment

The first step in creating a logical standby database is to follow the steps earlier in the chapter in order to create a physical standby database. In addition, you must make sure that supplemental logging is enabled on the primary database. If supplemental logging has not been enabled, it can be enabled via the ALTER DATABASE ADD SUPPLEMENTAL LOG DATA (PRIMARY KEY, UNIQUE INDEX) COLUMNS statement. This creates additional logging data that will be used by the SQL Apply service.
Once these steps have been done, you are ready to activate the logical standby database by performing the following steps:

1. Prepare primary and standby databases for role transition by setting up init params to take effect on role reversal. On primary and standby, set LOG_ARCHIVE_DEST_1,2,3 and LOG_ARCHIVE_DEST_STATE_1, 2, 3, and UNDO_RETENTION=3600 (for the LogMiner dictionary). On standby, set PARALLEL_MAX_SERVERS=9.(minimum). Issue a SHUTDOWN IMMEDIATE on the standby.
2. Create a logical standby control file with ALTER DATABASE CREATE LOGICAL STANDBY CONTROLFILE AS 'filename';
3. On standby, issue STARTUP MOUNT PFILE=<cpfile>;
4. Prepare the standby database for SQL Apply by running the SQL statement ALTER DATABASE RECOVER MANAGED STANDBY DATABASE.
5. Activate the logical standby database by running the SQL statement ALTER DATABASE ACTIVATE STANDBY DATABASE.
6. Run the nid (DBNEWID) utility in order to change the name of the database on the standby server (requires SHUTDOWN IMMEDIATE and STARTUP MOUNT).
7. Change the database name DB_NAME in the parameter file to that used in DBNEWID.
8. Create SPFILE for logical standby, and restart the database with ALTER DATABASE OPEN RESETLOGS.
9. Change the standby database global name using the SQL statement ALTER DATABASE RENAME GLOBAL_NAME TO newname.
10. Create new temporary files as you did with the physical standby database.
11. Start SQL Apply with the SQL statement ALTER DATABASE START LOGICAL STANDBY APPLY.

### Post-Deployment

Once a basic physical standby database has been created, there are a few more optional tasks that can be performed. Of course, this includes testing the standby database. There are a number of ways that the standby database can be monitored. These include the following Oracle tables and dynamic performance views:

- **DBA_LOGSTDBY_LOG**  This table provides information on redo log files that were registered on the standby system.
- **DBA_LOGSTDBY_PROGRESS**  This table provides statistics on the overall progress of SQL Apply.
- **V$LOGSTDBY_STATS**  This view provides information on LogMiner statistics.
- **V$LOGSTDBY**  Provides a snapshot of information about the log Apply process.

As with a physical standby database, you can change the data protection mode. These are the same data protection modes that are used with the physical standby database (described earlier) and are maximum protection, maximum availability, and maximum performance.

In addition to setting the data protection mode, it is always a good idea to test and verify the operation of the standby database.

### Summary

In addition to the information provided here, there is much more that can be configured and tuned with Oracle Data Guard. There are many options and many modes of operation that can be configured. How you configure your system depends on your needs and requirements. As with many Oracle features such as Oracle RAC, deploying Data Guard in a Linux environment is all about the details. Careful planning and testing will make your deployment successful.

![](img/9479df2d00f5e62b87366b125224950f_370_0.png)

## CHAPTER 14

Oracle Advanced Replication on Linux

Replication is the process of taking a database, table, or subset of those or other Oracle objects and copying them to another system automatically. Replication can be configured to work on an entire database or just a subset of the database. Regardless of how much or how little data there is to replicate, the functions and mechanisms are the same. This chapter will examine the methods that Oracle uses to replicate data from one system to another.

Although the end result might look similar to Oracle Data Guard, replication is actually quite different. Replication is designed to create one or more copies of a database or subset of the database. These copies are designed to be open and available to users. Replication can also be used in a bidirectional manner, where there are multiple masters. Data Guard is designed as a disaster recovery system, whereas replication is not primarily designed for DR. Data Guard works by transfer and applying redo data from the primary to the standby system, whereas replication is API- or trigger-based.

![](img/9479df2d00f5e62b87366b125224950f_371_0.png)

**NOTE**
Whereas Data Guard requires Oracle Enterprise Edition, replication comes with Standard Edition.

## Introduction to Oracle Replication

Oracle Advanced Replication is composed of processes and utilities that work together to configure, deploy, and maintain database objects on different systems throughout your enterprise. Replicated objects can reside in a database on the same computer system as the source database, or they can reside on systems thousands of miles away. The replicated objects can be configured to be read-only or read/write, depending on your needs and preferences. Advanced Replication is Oracle’s implementation of replication. In this chapter, the term replication will be used to describe advanced replication.

Oracle Advanced Replication is used for a number of purposes. It can be used to replicate read-only data that must be locally available to remote locations, such as stores. In this manner, you can replicate price data, parts details, documentation, etc., to each store, where that data can be readily available even when network problems might prevent communication to the main data center. This data can be used autonomously at each store, and only sales data needs to be sent back to the main data center. This will allow stores to keep running if the network is down or if there are problems with the main corporate systems.

In addition to availability, in this case replication can also provide for greater performance, since the data is located locally and can be quickly accessed by the
