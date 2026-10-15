
![](img/d95c931f4f3da4a6bd0ee55148fefad7_173_0.png)

Figure 5-7 Generated backup statements

Another way to backup the database is to generate the scripts through the Control Center and use your own scheduler to run this backup script periodically.

![](img/d95c931f4f3da4a6bd0ee55148fefad7_174_0.png)

## 5.1.6 Backup database in DB2 command line processor

In Example 5-12 we show you a script to backup our sample database ITSODB, which is partitioned. Call this script with the db2_all command:

```
db2_all '/db2home/db2inst1/database_backup.ksh db2inst1 itsodb'
```

### Example 5-12 Backup script database_backup.ksh

```
#!/usr/bin/ksh
#
# Script: backing up database
#---------------------------------------------

echo running against instance: ${1}
echo running against database: ${2}
INSTANCE=$1
DB_ALIAS=$2
#---------------------------------------------
# check for db2profile and execute it, if available
```

```
#-------------------------------------------------------------

DBHOME=`finger -l $INSTANCE | grep Directory | awk '{print $2}'`

if [ ! -f /$DBHOME/sqllib/db2profile ]
then

echo "File not found: " /$DBHOME/sqllib/db2profile
echo "please check host- and instancename"
echo " **************** script abnormally ended *******************"

exit 1

fi

. /$DBHOME/sqllib/db2profile

for i in 1 2 3
do
echo ""
echo "Start backing up database $DB_ALIAS on node $DB2NODE "
echo ""

db2 backup db $DB_ALIAS to /db2backup with 4 buffers parallelism 2

if [ $? = '0' ]
then
szDate=$(date)
echo ""
echo "backing up database $DB_ALIAS on node $DB2NODE successfully $szDate" |
tee -a /$DBHOME/$DB_ALIAS.log
echo ""
exit 0
fi

if [ "$i" -le "3" ]
then
echo "Start another trial"
fi
done
szDate=$(date)
echo ""
echo "backing up database $DB_ALIAS on node $DB2NODE failed after 3 trials $szDate " | tee -a /$DBHOME/$DB_ALIAS.log
echo ""
exit 8
```

Modify this sample so that it fits your environment and requirements.

Note: For a detailed explanation of backing up databases, refer to Chapter 2 "Database Backup" in IBM DB2 UDB Data Recovery and High Availability Guide and Reference V8, SC09-4831.

## 5.1.7 DB2 database recovery utility

A full or partial database restore may be required in many situations. The recovery method that is available depends on your backup and DB2 log handling. DB2 supports the following recovery methods:

- **Crash recovery**
DB2 uses this method to set a database to a consistent state after an unexpected failure. Crash recovery will rollback all the uncommitted changes. It can be forced with the `db2 restart database` command.
- **Full database restore offline**
This will restore the entire database to the point in time when the database backup was taken, or in conjunction with roll forward to a specific point in time. It is the only restore method to recover a database with circular logging. A full database restore example is:
`db2 restore db itsodb from /db2backup taken at 200210291525`
- **Full database restore with incremental**
Once your database is enabled for recovery, that is, log retain on, and for incremental backup, that is, trackmod is on, you can restore the entire or partial database to a point in time where it is needed.
`db2 restore db itsodb online incremental auto from /db2backup taken at 200210291525`
- **Tablespace restore**
If you have enabled roll forward recovery, it is possible to restore any tablespace to a point in time or to the end of log.
`db2 restore db itsodb "tablespace(nation_tsp)" online incremental auto from /db2backup taken at 200210291525`
- **Rollforward recovery**
This process applies changes to the tablespaces from the archive or active logs. This command must be issued from the catalog partition.
`db2 'rollforward db itsodb to end of logs on dbpartitionnum(0,1) and complete online'`

- Recovering a dropped table

DB2 supports the recovery of a dropped table by using tablespace level restore, if the tablespace where the table resides is enabled for dropped table recovery. This can be done during tablespace creation or by altering an existing table using the DROPPED TABLE RECOVERY ON option.

> Note: For a detailed explanation of backing up databases, refer to Chapter 2 "Database Backup" in IBM DB2 UDB Data Recovery and High Availability Guide and Reference V8, SC09-4831.

## 5.1.8 Backup and restore sample scenario

The following scenario is applied to our four partition database ITSODB:

- After creating and loading many tables into the database, we take a full offline backup.
- Roll forward, userexit, and trackmod are enabled.
- Normal usage of the database starts which includes updates, delete, and so forth against tables.
- Online incremental backups are regularly scheduled.

We perform the following activities in sequence to demonstrate the database restore functions:

- 1. Full offline database backup of ITSODB
- 2. Updates against table CUSTOMER
- 3. Full online incremental database backup of ITSODB
- 4. Updates against table CUSTOMER
- 5. Full online incremental database backup of ITSODB
- 6. Updates against table CUSTOMER
- 7. Table CUSTOMER is no longer accessible after a system outage of host udblnx05, where database partitions 2 and 3 are located.

To restore our table to the point in time right before it was corrupted, you have to find out when the last backup was taken. To do this, we issued the following command on each partition (which is partition 2 and 3 in our example):

```
db2 list history backup all for itsodb
```
