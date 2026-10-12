
## Read Consistency

Read consistency is the attribute that allows multiple processes to read from the database and achieve a consistent view of the data. When a process begins to read the data from the database, the data it gets is consistent as of the point of time when the statement began.

For example, if a statement begins to read data from a table, and in the middle of the action to read that data, some of that data is modified by a different process, the original unmodified data is read. This provides a consistent view of the data. Within the Oracle RDBMS, this is achieved via the undo records. When data is modified, the original data is saved within the undo records until both the statement that has modified the data has been committed and all other processes that might read that data have completed.

Since this view is consistent as of the start time of the statement, there might be several different versions of the same data stored in the undo records. This provides a high-performance method of achieving read consistency.

## Data Integrity

Certain functions are absolutely essential for the proper functioning of the database server. Among these is data integrity, recovery from failure, error handling, and so on. The following sections list and describe some of these functions.

## Checkpoints

When writing to the database, changes are made in the buffer cache within the SGA and written out to the database files later by the DBWR process. This is done using an LRU (Least Recently Used) list algorithm. Because recently used data might never go to the end of the LRU, Oracle must somehow make sure that dirty or modified buffers eventually get written out. This is to assure the integrity of the database and shorten the recovery time (in the event of a failure). Oracle does this with a mechanism called a checkpoint.

![](img/9479df2d00f5e62b87366b125224950f_97_0.png)

The checkpoint process makes sure that the dirty buffers are eventually written out to disk. Oracle uses either the CKPT background process or the LGWR process to signal a checkpoint. But what is a checkpoint and why is it necessary?

Because all modifications done to data blocks are done on the block buffers, there are changes to data in memory that are not necessarily reflected in the blocks on disk. Because caching is done using a least-recently-used algorithm, if a buffer is constantly modified, it is always marked as recently used and is therefore unlikely to be written out by the DBWR.

A checkpoint is used to ensure that these buffers are written to disk by forcing all dirty buffers to be written out on a regular basis. This does not mean that all work stops during a checkpoint; the checkpoint process has two methods of operation: the fast checkpoint and the normal checkpoint.

In the normal checkpoint, the DBWR merely writes out a few more buffers every time it is active. This type of checkpoint takes much longer but has less of an effect on the system. In the fast checkpoint, the DBWR writes a large number of buffers at the request of the checkpoint each time it is active. This type of checkpoint completes much quicker and is more efficient in terms of I/Os generated, but it has a greater effect on system performance at the time of the checkpoint.

You can use the time between checkpoints to improve instance recovery. Frequent checkpoints reduce the time required to recover in the event of a system failure. A checkpoint automatically occurs at a log switch.

## The Redo Log

Redo Log files are used to store redo information. Each time data is changed in the database, a log record is written describing these changes. With this information, the database can be recovered in the event of a system failure, by replaying committed transactions and rolling back uncommitted transactions.

If a catastrophic system failure occurs, as with a power failure, component failure, and so on, the Oracle instance can be aborted. Thus, it will either immediately be cut off, or in the event of a disk failure, the instance may crash. If this occurs, all changed data in the buffer cache will be lost; only changes that have been written out to disk will be saved.

When Oracle is restarted, the information in the redo log file is used to replay all changes that have been made to the database since the last time the datafiles were written to. All previously committed transactions will be recovered, something known as rolling-forward. All transactions that had modified data but have not been committed will be rolled back. This is known as rolling-back. Rolling-back is similar to the operation that would be executed if you were to issue a ROLLBACK statement rather than a COMMIT at the end of a transaction.

This redo log file is necessary for proper recovery. If the redo log file is lost, due to a disk failure, you will not be able to recover in the event of a system failure. Because of this, the redo log file must be protected against this kind of failure. I recommend that disk mirroring or RAID1 be used on all redo log files.

## Protect the Redo Log

If you use a write-cache on the controller that has the redo log files and it is not battery backed-up, you are in danger of losing data. In the event of a power failure, you will lose redo information and may not be able to recover.

Since the redo log files are so critical to the recoverability of the system, it is recommended that you do not use a caching disk controller with write-caching unless that cache is battery backed-up. In the event of a power failure, you must make sure no redo information is lost. It is often recommended that write-caching not be used at all on the redo log, but I feel that if the write cache is protected by battery back-up, your risk is reduced and write-caching is acceptable.

## How the Redo Log Works

Each change to the database is logged into the redo log. Because of this, in the event of a failure, all changes made since the last backup can be recovered with the use of these redo log files. If the instance should fail, due to a power failure or other system failure, the redo log files can recover all changes done since the last checkpoint.

When a COMMIT operation is performed, the redo information is written into the redo log buffers. The LGWR process writes the redo log files with the information in the redo log buffer. The COMMIT operation is not completed until the redo log has been written. Once this has occurred, that transaction is irrevocable and will be recovered in the event of a system failure. Thus, you can see how important the redo log file really is.

The redo log is made up of two or more redo log files or log file groups. A log file group is a set of files that Oracle uses for redundancy. A redo log group is treated as if it were one redo log file; however, it is redundant. In this manner, the redo log is protected against disk failure. A redo log group is made up of one or more redo log files and must be protected against disk failure. If you are using disk mirroring to protect the redo log, it is not necessary to use redo log file groups. Since the disk is protected, single log files are sufficient. Most people choose to take advantage of a hardware

RAID system rather than use Oracle mirroring due to the performance benefits of hardware RAID over Oracle mirroring.

The redo log has two or more log files or log file groups that are used in an alternating fashion. Once the first log file has filled up, the logging operation moves to the next redo log file in the chain. If archiving is enabled, when it fills up and the log switch occurs, this file is copied to an *archive log file*. These archive log files are very important for the recoverability of the system in the event of a catastrophic failure.

Operations on the redo log files are done with the **ALTER DATABASE** command. Using the **ALTER DATABASE** command, you can add redo log groups and redo log files, rename redo log files, and perform other tasks.

## Checkpoints

A checkpoint causes all in-cache data blocks that have been modified and not been written out to disk to be written to the disk. These unwritten changed buffers are called <I>dirty buffers</I>. Dirty buffers are what cause the system to be recovered since data might have been changed in memory and committed, but not written out to disk. In addition, there might be changes that have been written out to disk, but not yet committed.

### Log Switches and Checkpoints

Each time a redo log file or log file group fills up, it switches to the next redo log file in the sequence. This switch, called the *log switch*, causes several automatic events to occur. They consist of:

- **The checkpoint** A log switch always causes a checkpoint to occur, which flushes all dirty buffers from the Oracle buffer cache. This reduces the amount of time a recovery will take, if needed.
- **Archiving** If archiving is turned on, and it should be, the log switch causes the redo log file that was just active, to copy its contents to an *archive log file*. This archive log file is used in recovery if needed.
- **The log sequence number** Each time a redo log file is reused, it is given a *log sequence number*. This *log sequence number* is also given to the associated archive log file.

Archiving and checkpointing are integral parts of the Oracle RDBMS functionality and are critical to system recoverability and stability.

### Log Switch and Checkpoint Intervals

The initialization parameters **LOG_CHECKPOINT_INTERVAL** and **LOG_CHECKPOINT_TIMEOUT** can be used to control the checkpoint interval. The parameter **LOG_CHECKPOINTS_TO_ALERT** is used to print a message into the alert log whenever a checkpoint occurs. This is nice for seeing when checkpoints are happening, but can easily create extremely large amounts of alert log space.

### LOG_CHECKPOINT_INTERVAL

The **LOG_CHECKPOINT_INTERVAL** is set to a number of operating system blocks that are used before the log switch occurs. For most operating systems, the size of the blocks is 512 bytes. So, this parameter will set the number of 512-byte blocks used in the redo log before a checkpoint occurs.
