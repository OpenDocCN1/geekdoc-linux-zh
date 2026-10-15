Local Database Directory on /database

Number of entries in the directory = 1

Database 1 entry:

Database alias               = ITSODB
Database name                = ITSODB
Database directory           = SQL00001
Database release level       = a.00
Comment                      = ITSO San Jose
Directory entry type         = Home
Catalog database partition number = 0
Database partition number    = 0

db2inst1@udblnx02:> db2 redistribute database partition group mpl_01 uniform
DB20001I  The REDISTRIBUTE NODEGROUP command completed successfully.
db2inst1@udblnx02:>

For each table that has already been processed, the redistribution utility writes a message to file in $INSTHOME/sqllib/redist/<dbmame>.<part-group>.<time>. See Example 3-29.

# Example 3-29 Redistribute messages file

```
Data Redistribution Utility

--------------------------------

The following options have been specified:
Nodegroup name            : MPL_01
Data Redistribution option : U
Redistribute Nodegroup    : Uniformly
No. of nodes to be added  : 1
List of nodes to be added :
2
No. of nodes to be dropped : 0
List of nodes to be dropped :

Delete will be done in parallel with the insert.

The execution of the Data Redistribution operation on:

Begun at   Ended at   Table
--------   --------   ------------
15.29.38
15.32.13   DB2INST1.CUSTOMER
15.32.16
15.32.16   DB2INST1.NATION
```