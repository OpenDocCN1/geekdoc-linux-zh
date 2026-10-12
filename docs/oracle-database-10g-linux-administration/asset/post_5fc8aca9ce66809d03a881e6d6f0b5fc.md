
is constantly modified, it is always marked as recently used and is therefore unlikely to be written out by the DBWR for a long time. The time it takes to perform instance recovery in the event of a failure is dependent on how many dirty buffers were in the buffer cache at the time of the failure.

The checkpoint process is used to ensure that these "dirty" buffers are written to disk periodically by forcing all dirty buffers to be written out on a regular basis. This does not mean that all work stops during a checkpoint; the checkpoint process has several methods of operation: the incremental checkpoint, fast-start checkpointing, and normal checkpoints.

The checkpoint itself is the point in the log file that is the starting point for instance recovery. In order to speed recovery, there are several mechanisms that control how checkpoints are done, and thus different recovery intervals.

With Oracle 10g, an incremental checkpoint is automatically enabled. This is known as automatic checkpoint tuning. With automatic checkpoint tuning, idle times are used to write data out to disk, thus advancing the checkpoint. This takes advantage of idle times, thus reducing the effect on system performance, but isn't very reliable in terms of recovery time.

For a more predictable recovery time, enable fast-start checkpointing by setting the FAST_START_MTTR_TARGET initialization parameter to a value other than 0. This parameter is used to specify the number of seconds instance recovery should take. The lower the value of this parameter, the more aggressive the checkpoint operation. Fast-start checkpointing tags on additional writes to the DBWR operations. The more aggressive the recovery interval, the more aggressive the additional writes. However, it is always better to enable fast-start checkpointing, even if you specify the maximum value for FAST_START_MTTR_TARGET of 3600 seconds.

Fast-start checkpointing is overridden by setting the LOG_CHECKPOINT_INTERVAL initialization parameter. This parameter specifies how many operating system blocks of data can be written to the redo log since the last incremental checkpoint before a traditional checkpoint is initiated. If this value is reached, all dirty blocks in the buffer cache will be written out to disk. The initialization parameter LOG_CHECKPOINT_TIMEOUT can also be set. This parameter specifies the amount of time in seconds since the last incremental checkpoint that can pass before a checkpoint is issued.

Reducing the time between checkpoints improves instance recovery. Frequent checkpoints reduce the time required to recover in the event of a system failure. In addition to the checkpoints that are triggered by the number of OS blocks or time since the last checkpoint, checkpoints automatically occur at a log switch as well.

## Logging and Archiving

The redo log records all changes made to the Oracle database. The purpose of the redo log is to ensure that, in the event of the loss of a data file caused by some sort of system failure, the database can be recovered. By restoring the data files back to a known good state from backups, the redo log files (including the archive log files) can replay all the transactions to the restored data file, thus recovering the database to the point of failure.

When a redo log file is filled in normal operation, a log switch occurs and the LGWR process starts writing to a different redo log file. When this switch occurs, the ARCH process copies the filled redo log file to an archive log file—this is how Archiving works (if you are running in NOARCHIVELOG mode, these files will be discarded). When this archive is complete, the redo log file is marked as available. It is critical that this archive log file be safely stored because it may be needed for recovery. This is why ARCHIVELOG mode is critical for production systems.

![](img/9479df2d00f5e62b87366b125224950f_310_0.png)

> **NOTE**
> Remember that a transaction has not been committed until the redo log file has been written. Slow I/Os to the redo log files can slow down the entire system.

### ARCHIVELOG Mode

The Oracle RDBMS is not required to run in ARCHIVELOG mode. In NOARCHIVELOG mode, archiving of redo logs does not occur. If you do not run in ARCHIVELOG mode, it is impossible to recover any transactions that are not in the current redo log files. Normally, a database is created in NOARCHIVELOG mode and then altered to ARCHIVELOG mode after creation. Putting a database in ARCHIVELOG mode starts the ARCH background process.

![](img/9479df2d00f5e62b87366b125224950f_310_1.png)

> **NOTE**
> If you do not run in ARCHIVELOG mode, you will most likely lose valuable data in the event of the loss of a data file. It is always recommended that production systems be run in ARCHIVELOG mode. You may run test systems without archiving, unless doing performance benchmarking, in which case you will want to run in ARCHIVELOG mode to factor in the additional overhead.

### Enabling Archiving

Archiving is enabled by running ALTER DATABASE command with the parameter ARCHIVELOG in MOUNT mode.

To permanently enable archiving, use

```
ALTER DATABASE ARCHIVELOG;
```

To automatically begin archiving only for the current startup, enter the SQL*Plus command **ARCHIVE LOG START** in MOUNT or OPEN mode.

### Disabling Archiving

To permanently disable archiving, use the following command in MOUNT mode:

```
ALTER DATABASE NOARCHIVELOG;
```

If you are in ARCHIVELOG mode and want to disable it for a particular startup, issue the **ARCHIVE LOG STOP** command.

### Listing Archive Log Status

The following SQL*Plus command shows the range of redo log files to be archived, the current log file group's sequence number, and the current archive destination.

```
SQL> ARCHIVE LOG LIST
```

If you are using both ARCHIVELOG mode and automatic archiving, the display will look something like this:

Database log mode          Archive Mode
Automatic archival          Enabled
Archive destination         /opt/oracle/admin/PROD/arch
Oldest online log sequence  221
Next log sequence to archive 222
Current log sequence        222

### Setting the Archiving Destination

With Enterprise Edition, the Oracle parameter **LOG_ARCHIVE_DEST_n** (where *n*= 1, 2, 3, ..., 10) sets up to ten archive log destinations for Oracle archiving. Typically, **LOG_ARCHIVE_DEST_1** is used for the local archive destination. The form **LOG_ARCHIVE_DEST** (without the numbers) has been deprecated in Oracle 10g Enterprise Edition. With standard edition, **LOG_ARCHIVE_DEST** is still used. Archive log files will be created in the directory with a different filename for each archive log file. This filename is defined by the Oracle parameter **LOG_ARCHIVE_FORMAT**. Both of these parameters are described in the Oracle documentation.

### Comparing ARCHIVELOG mode and NOARCHIVELOG mode

Although NOARCHIVELOG mode might seem to be more economical, it is unwise to run in NOARCHIVELOG mode under most circumstances. The following table describes the differences in the two modes.

| Log Mode | Recoverability | Performance | Disk Space | Notes |
| :--- | :--- | :--- | :--- | :--- |
| ARCHIVELOG | Point of failure | Archive log overhead | Significant | Recommended |
| NOARCHIVELOG | Last backup | No additional overhead | No additional disk space | Benchmarks, development, testing only |

Because of the lack of recoverability, NOARCHIVELOG mode is not recommended for any production environments.

## Introduction to Backup

There are a variety of options available for backing up the Oracle database. Each option provides a different amount of protection and typically causes a different amount of downtime. These options are as follows:

- **Backup Type**
  - Archivelog backup: A backup of the archive log files
  - Controlfile backup: A backup of the control files
  - Datafile backup: A backup of a single datafile
  - Full backup: A backup of all datafiles and control files
  - Tablespace backup: A backup of a single tablespace
  - Incremental backup: A backup of data that has changed since the last backup

In this section, you will learn how each of these backup types differ, how to perform them, and how they complement each other. In addition, most of these backup types can be completed either by using traditional Oracle backup methods or by using Oracle RMAN (Recovery Manager).

### Archivelog Backup

As archive log files are continually being created, these files are periodically backed up to offline storage and purged from both disk and tape in accordance with retention policies dictated by the business’ SLA. Since the archive log information can be quite large (logs can range from 10MB each to over 1GB for databases with high volume, and they usually are tuned to switch at least every half hour), it is usually not feasible to keep this data online indefinitely. If possible, you should keep all
