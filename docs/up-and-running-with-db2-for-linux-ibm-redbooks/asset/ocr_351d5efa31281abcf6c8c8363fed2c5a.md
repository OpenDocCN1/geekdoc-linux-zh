```
Mon Oct 21 17:06:28 PDT 2002
udb1nx02: date completed ok

Mon Oct 21 17:16:35 PDT 2002
udb1nx05: date completed ok

Mon Oct 21 17:16:35 PDT 2002
udb1nx05: date completed ok
```

Now you are able to start DB2 in a multiple host, multi-partitioned environment. To do this, enter the db2start command on any host. Refer to Example 3-6.

# Example 3-6 Start of a DB2 instance with four partition

```
db2inst1@udb1nx02:> db2start
11-01-2002 15:10:51  1  0  SQL1063N  DB2START processing was successful.
11-01-2002 15:10:51  0  0  SQL1063N  DB2START processing was successful.
11-01-2002 15:10:52  3  0  SQL1063N  DB2START processing was successful.
11-01-2002 15:10:53  2  0  SQL1063N  DB2START processing was successful.
SQL1063N  DB2START processing was successful.
```

> Note: db2_all is a shell script provided by DB2 that allows you to send commands to one or all database partitions.

# 3.3 Creating a database

When you create a database, the following tasks will be done for you:

+   - Setting up of all the system catalog tables that are required by the database
+   During creation of a new database, DB2 allocates three tablespaces: SYSCATSPACE, USERSPACE1 and TEMP SPACE1. The tablespace SYSCATSPACE holds all system catalog tables. These catalog tables are actually a repository that keeps information and statistics about all objects within the database. USERSPACE1 contains the tables for holding user created tables. A system temporary tablespace (TEMP SPACE1) is required by DB2 to support activities like sorting data, join tables create indexes.

+   - Allocation of the database recovery log
+   The DB2 recovery log tracks all changes made against your database. It is also called the transaction log. It is used with the recovery history file to recover data in case of failure.