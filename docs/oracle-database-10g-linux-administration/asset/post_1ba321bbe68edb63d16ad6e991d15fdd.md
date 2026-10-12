
Specify a larger block size than with rcp or scp. With Linux, the following command is very efficient for copying data files from one system to another:

```
dd bs=64k if=<data file spec> | ssh_standby "( dd bs=64K of=<data file spec>)"
```

If you are using OCFS, make the following modification to the preceding command:

```
dd -O_DIRECT=64k if=<data spec> | ssh_standby " 
( dd -O_DIRECT=64k of=<data file spec>)"
```

Using dd can be ten times faster than using scp or rcp.

## Create a Control File for the Standby Database

Create the standby control file on the primary database using the ALTER DATABASE CREATE STANDBY CONTROLFILE AS '<filename>'. This standby control file will be copied to the standby database system that is described in this section. This standby control file must be created with the database in MOUNT mode, and after the latest timestamp for the backup datafiles.

## Create Standby Initialization Parameters

The parameter set for the standby server will be similar to that used on the primary server; however, a few of the parameters are set differently. The standby database must have a different DB_UNIQUE_NAME from the primary server. In addition, the FAL_CLIENT and FAL_SERVER parameters are reversed on the standby database server. Other parameters specific to Data Guard include LOG_ARCHIVE_DEST_2, LOG_ARCHIVE_DEST_STATE_2, LOG_ARCHIVE_CONFIG, and STANDBY_FILE_MANAGEMENT.

A new feature of Oracle 10g is that parameters like LOG_ARCHIVE_DEST_2, formerly requiring that they be changed on role reversal, now have additional attributes to specify what role they apply to. This allows the same initialization parameter file to be used on each site (though it must be different between sites), regardless of database role.

**Tip**
*It is often much easier to create a PFILE and use the PFILE for the initial configuration steps. Once the standby server has been set up correctly, an SPFILE can be created.*

## Copy Files to the Standby Server

Next, copy the backup files (if you haven't already done this as part of the backup process itself as shown earlier in this chapter), the standby control file (copy to same locations and name as the primary controlfiles), and the initialization parameter file to the standby system. In order to create identical primary and standby sites, you also need to copy initialization scripts for environment setup (such as .profile and other scripts), as well as DBA scripts. These files can be copied via scp or sftp or by using an NFS-mounted volume. As mentioned earlier in this chapter, the /etc/oratab file should be copied as well. And unless you are installing Oracle 10g on the standby site from scratch using the OUI, you will also need to copy the ORACLE_HOME directory, the admin directory (including subdirectories bdump, cdump, create, pfile, and udump), and the /etc/hosts file to the standby site (you may need to add new entries to the /etc/hosts file for any new NICs dedicated to redo traffic). The network parameters can be important when configuring your system for Data Guard.

As mentioned previously, the data files can be copied as part of the backup process itself, as shown here:

```
dd bs=64k if=<data file spec> | ssh standby "( dd bs=64k of=<data file spec>)"
```

If you are using OCFS, make the following modification to the preceding command:

```
dd -O_DIRECT=64k if=<data file spec> | ssh standby "
(dd -O_DIRECT=64k of=<data file spec>)"
```

As was mentioned, using dd can be ten times faster than using scp or rcp.

Finally, synchronize OS clocks. Not doing so can make it very confusing later on when comparing log files (particularly alert logs) containing timestamps, because they will probably not dovetail. If servers are not already synchronized, you may want to ask the Systems Administrator to implement enterprise-wide synchronization software such as NTP to keep all server clocks synchronized all the time.

## Set Up the Network Environment

Once all of the needed files are on the standby server, configure an Oracle network service name for listeners configured for the primary and standby databases for log transport services to use. Configuration files include listener.ora, tnsnames.ora, and sqlnet.ora files. On the primary site, either use a second connect string for redo data on the current database listener, specifying a different port, or create a separate listener than that used to connect to the primary database. Do the same on both systems in preparation of a role switch. Also add aliases to the tnsnames.ora files for redo log transfer. You will probably want to use the Oracle Net parameter SDU (session data unit) in the tnsnames.ora file to set the transport size to 32k. For more information, see *Data Guard Concepts and Administration, 10g Release 1, Section A.6*. To enable broken connection detection, set SQLNET.EXPIRE_TIME = 2 (in minutes) as recommended by Oracle. When configuring the Oracle Net service, the SQLNET.EXPIRE_TIME needs to be set in the sqlnet.ora file.

## Additional Steps

At this point, the following optional steps can be done (if desired):

- Create standby redo logs (SRLs). This step is highly recommended for all protection modes, even maximum performance mode. The standby redo log files are created using the ALTER DATABASE command, as shown here:

```
SQL> ALTER DATABASE ADD STANDBY LOGFILE THREAD 10
2> ('<log file spec 1>', '<log file spec 2>') SIZE 100M;
```

- Create/clean the online redo log files on the standby to prepare for role reversal (optional). When the standby becomes the primary, the online redo log files are created for you automatically. This step can be done ahead of time by creating the redo log files on the standby system. This is done very easily via the ALTER DATABASE CLEAR LOGFILE statement. This is done as follows:

```
ALTER DATABASE CLEAR LOGFILE GROUP 1;
ALTER DATABASE CLEAR LOGFILE GROUP 2;
...
ALTER DATABASE CLEAR LOGFILE GROUP n;
```

- Start the DG Broker. Start the Data Guard monitor (DMON) process on each site by setting the initialization parameter DB_BROKER_START to TRUE on both sites. You now need to create and enable the broker configuration.

- Enable Flashback Database as additional protection.

## Start the Standby Database

The database is almost ready to begin functioning as a standby database; however, the standby database requires additional temporary space. All temporary tablespaces and data on the primary site file should be created on the standby site. You can use the CREATE TEMPORARY TABLESPACE command(s) on the standby database from the text controlfile created on the primary from running ALTER DATABASE BACKUP CONTROLFILE TO TRACE. To create a temporary tablespace, the standby database needs to be started in read-only mode using the command STARTUP OPEN READ ONLY. In this mode, additional temp files can be added to the database.

At this point, you are ready to begin standby mode. This is done by starting the Redo Apply by issuing the SQL command ALTER DATABASE RECOVER MANAGED STANDBY DATABASE DISCONNECT [FROM SESSION]. The DISCONNECT statement makes this command run in a background session.

## Test the Standby Database

The Data Guard log transport and apply services can be tested by issuing an ALTER DATABASE SWITCH LOGFILE command on the primary server and making sure that the redo data is transmitted and applied to the standby server. In addition, the following steps can be used to validate that Data Guard is working properly:

1. Identify existing archived log files on the standby:
   - SELECT SEQUENCE#, FIRST_TIME, NEXT_TIME FROM
   - V$ARCHIVED_LOG ORDER BY SEQUENCE#;

2. Force a log switch on the primary to archive the current online redo log file:
   - ALTER SYSTEM ARCHIVE LOG CURRENT;

3. Verify new redo data was archived on the standby:
   - SELECT SEQUENCE#, FIRST_TIME, NEXT_TIME FROM
   - V$ARCHIVED_LOG ORDER BY SEQUENCE#;

It is important to validate that Data Guard is functioning properly before continuing. Don't assume that everything is working properly.

## Post-Deployment

Once the basic physical standby database has been created, there are a few more optional tasks that can be performed. Now, you should create the temporary data files. Additional temp datafiles should be created; one for each temp datafile that you currently have in the database. This is done as follows:

```
STANDBY> ALTER TABLESPACE TEMP ADD TEMPFILE
'D:\oracle\oradata\stby\temp02.dbf'
SIZE 20M REUSE;
```

The new temp datafiles are used in the event that the standby becomes the primary.

If you wish, you can change the data protection mode. As mentioned earlier, these are data protection modes that can be used:

- **Maximum protection** In this mode, a transaction is not committed on the primary server until it has been written into the primary server's redo log as well as at least one standby redo log.

- **Maximum availability** This mode is similar to the maximum protection mode; however, transaction processing on the primary server does not stop in the event of a failure.

- **Maximum performance** This is the default mode; it transfers data to the standby redo log files in an asynchronous fashion.

In addition to setting the data protection mode, it is also a good idea to test and verify the operation of the standby database.
