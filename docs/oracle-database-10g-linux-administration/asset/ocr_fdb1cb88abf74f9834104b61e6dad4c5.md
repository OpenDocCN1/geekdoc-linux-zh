Restoration Restoration is the act of replacing a datafile with a backup copy. If you are running in ARCHIVELOG mode, you can restore up to the point of failure. If you are not running in ARCHIVELOG mode, you can only restore back to your last backup.

Typically, recovery is automatic, with the recovery process prompting you to apply archived log files if necessary. The act of restoring is a manual operation where operator intervention is required either by hand or with the graphical administration tools.

In this chapter, you will learn both how recovery works and how to restore damaged datafiles.

# # How to Recover Your Database

As reliable as hardware has become today, there are still occasions when the system may fail. This may be due to a hardware component failure, or an external event such as a power failure. If the failure does not cause any data to be lost, Oracle can recover itself. This is referred to as an instance recovery. If data has been lost, it must be restored from a previous backup and recovered—a process known as media recovery. If some event has occurred, such as an accidental dropping of a table, a point-in-time recovery must be done in order to not recover the DROP TABLE statement and repeat the mistake.

In this section, you will learn how to perform each of these recoveries and how they work.

# ## Instance Recovery

When an instance failure occurs, the Oracle recovery process can completely recover the database upon instance startup. All transactions committed at the time of the failure will be recovered or *rolled forward* and all transactions that were in process (also known as *in-flight transactions*) will be *rolled back*.

> **NOTE**
> *Instance recovery can be quite time-consuming. The amount of time it takes depends on the number of dirty buffers in the SGA, and the number of dirty buffers depends on the amount of time since the last checkpoint and the amount of data modifications.*

The instance recovery process is automatic. When the instance is started up, it examines the datafiles and redo log files and determines whether the instance was shut down properly. At this point, the redo log will be read and the affected transactions will be rolled forward or rolled back. If the checkpoint launched by the last log switch had completed only the transactions in one log file, it alone will need to be recovered.