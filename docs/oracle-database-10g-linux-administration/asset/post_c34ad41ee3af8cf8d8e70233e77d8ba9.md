
## Instance Recovery

Instance recovery can be quite time-consuming. The amount of time that instance recovery takes depends on the number of dirty buffers in the SGA. The number of dirty buffers depends on the amount of time since the last checkpoint. The time it takes for instance recovery also depends on the recovery parallelism.

By tuning the checkpoint interval and recovery parallelism, the recovery time can be shortened. However, even with careful configuration, extremely long transactions can take a long time to roll back.

## Data Recovery or Media Recovery

Media recovery is necessary when media failure has occurred. For example, when a data file is damaged due to a disk failure or a software failure, or even some types of human error, you must first restore the damaged file from backup before you can recover it. The Oracle recovery process will then apply archive log files and redo log files to restore the damaged data file to its state just prior to the failure. All of the archive log files created since the last backup until the failure will be required to recover the restored data file. This process can be quite time-consuming.

> **NOTE**
> 
> By scheduling frequent backups, the restoration and recovery time can be shortened. The recovery time is proportional to the time between the last full backup and the time of failure, as well as to the amount of data that has changed since that backup.
> 
> By shortening the time between backups, the volume of data change since that backup can be minimized.

As you will see in this chapter, the goal is to have the shortest possible downtime in the event of a catastrophic system failure.

## Online and Archived Redo Log File Recovery

You cannot recover from the loss of an archived log file if a datafile also needs to be recovered. The sections that follow describe the steps to recover from the loss of an online or archived redo log file when the data files are intact. It is always recommended that redo and archived log volumes be created on fault-tolerant disk volumes, and that the redo log files be multiplexed within Oracle.

### Current Online Redo Log Recovery

Loss of one member of a current online redo log group will not cause the database to cease operations as long as another Oracle-multiplexed member of that group is not affected. Error information is written to the alert log and operation continues.

If all members of a redo log group are lost, you must do a point-in-time restore to the latest archived redo log extended through any redo logs not already overwritten. You can specify both these archived and valid online redo logs during recovery. Recovery from loss of all members of a current online multiplexed redo log group is done by executing a point-in-time recovery.

Mirroring the members of a redo log group to separate disks/controllers is optional, but Oracle strongly recommends operating with each member of a redo log group on separate disks, away from Oracle data files (three members in each group on separate disks under separate controllers, if feasible) to prevent a single point of failure.

### Inactive Online Redo Log Recovery

Loss of one member of an inactive online redo log file group will not cause the database to cease operations as long as another multiplexed member of that group is not affected.

You can recover from loss of a single member of an inactive online redo log group as follows:

- 1. If the instance is running, query the v$recovery_file view to find the file needing recovery; otherwise, do a startup, bring the instance to the MOUNT stage, and perform the query.
- 2. Shut down the instance normally.
- 3. Copy the archived log containing the sequence number of the missing/bad redo log to the location of the original redo log.
- 4. Issue the startup command.

You can recover from loss of an entire inactive online redo log group as follows:

- 1. If the instance is running, perform a normal shutdown.
- 2. Start the instance and bring it to the MOUNT stage.
- 3. Query the V$LOG view to ensure the log file has been archived.
- 4. Issue the command ALTER DATABASE CLEAR LOGFILE <file_name> for the bad redo log files. (Use the UNARCHIVED flag if the log file has not been archived.)
- 5. Delete the physical files at the OS level if necessary.
- 6. Issue the ALTER DATABASE DROP LOGFILE GROUP command.
- 7. Issue the ALTER DATABASE ADD LOGFILE GROUP command with the desired naming and storage for the initial log member in the group.
- 8. Add other redo log file members to the group as necessary.
- 9. Issue the ALTER DATABASE OPEN command.

## Archived Redo Log Recovery

Loss of an archived redo log file does not affect the current operation of the database, but it can impact the ability to do either full or incomplete (i.e., point-in-time) recovery.

If there is little or no likelihood of needing to perform point-in-time or incomplete recovery, the simplest method of resolving this situation is to perform an immediate full backup. This eliminates the need for the archived redo log files that were created prior to the full backup. This will also allow for full recovery to a time beyond the lost archived redo log from the full backup datafiles.

If there is a possible need to do point-in-time or incomplete recovery, and if a backup of the archived redo log exists on other media (e.g., as a tape backup), restore the lost archived redo log from tape to the archive destination. If no backup copy of the lost archived redo log exists, recovery will only be possible to the point in time of the last complete archived redo log prior to the one lost.

Oracle strongly recommends making a backup copy of the archived redo logs in order to prevent a single point of failure for recovery.

## How Transactions Work

Remember, the term transaction is used to describe a logical group of work. This group of work can consist of one or many SQL statements and must end with a commit or a rollback. Because this example assumes a client/server application, SQL*Net is necessary. The following steps are executed to complete the transaction:

- The application processes the user input and creates a connection to the server via SQL*Net.
- The server picks up the connection request and creates a server process on behalf of the user.
- The user executes a SQL statement and commits the transaction. In this example, the user changes the value of a row in a table.
- The server process takes this SQL statement and checks the shared pool to see whether there is a shared SQL area that has this identical SQL statement (assuming CURSOR_SHARING=EXACT). If it finds an identical shared SQL area, the server process checks to see whether the user has access privileges to the data. If the user has access privileges, the server process uses the shared SQL area to process the request. If a shared SQL area is not found, a new shared SQL area is allocated, and the statement is parsed and then executed.
- The server process retrieves the data from the SGA (if present) or retrieves it from the data file into the SGA.
- The server process modifies the data in the SGA. Remember that the server processes can only read from the data files. Because the transaction has been committed, the LGWR process immediately records the transaction in the redo log file. At some later time, the DBWR process writes the modified blocks to permanent storage.
- If the transaction is successful, a completion code is returned across the network to the client process. If a failure has occurred, an error message is returned.

![](img/9479df2d00f5e62b87366b125224950f_308_0.png)

> **NOTE**  
> *A transaction is not considered committed until the write to the redo log file has been completed. This arrangement ensures that in the event of instance failure, a committed transaction can be recovered. If a transaction has been committed, it is guaranteed to be recovered in the event of instance failure.*

While transactions are occurring, the Oracle background processes are all doing their jobs, keeping the system running smoothly. Keep in mind that while this process is going on, hundreds of other users may be doing similar tasks. It is Oracle's job to keep the system in a consistent state, to manage contention and locking, and to perform at the necessary rate.

It is because of the recoverability requirements that the redo log entries must be written out to disk before the commit operation can complete. If a failure occurs before that entry has been written, the transaction will not be recovered.

## RDBMS Functionality

If the Oracle database server is to provide data integrity features such as recovery from failure and error handling, it must provide a certain set of functions and procedures. The following sections list and describe some of these functions.

## Checkpoint

Because all modifications done to data blocks are done on the block buffers, there are changes to data in memory that are not necessarily reflected in the blocks on disk. Because caching is done using a least recently used (LRU) algorithm, if a buffer
