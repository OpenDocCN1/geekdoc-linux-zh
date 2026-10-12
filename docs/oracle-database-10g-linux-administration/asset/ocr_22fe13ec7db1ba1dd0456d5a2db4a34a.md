![](bbox=[0.05, 0.12, 0.13, 0.18])

# **TIP**

By tuning the checkpoint interval and recovery parallelism, recovery time can be shortened.

Once the instance recovery has finished, the database will be opened and users will again be allowed to access it. During the recovery process, users cannot access the database. It is for this reason that the recovery time should be as short as possible.

The parallel recovery feature of the Parallel Query Option can help reduce the time it takes for instance recovery to complete. This is done by setting the Oracle initialization parameter RECOVERY_PARALLELISM. By tuning the number of recovery processes to run best with your system, the recovery interval can be optimized.

# ## Media Recovery

Data recovery is necessary when media failure has occurred. For instance, when a datafile is damaged. In this case, you must first restore the damaged file with a good copy from a backup before recovery can occur. The Oracle recovery process will then apply archive log files and redo log files to restore the good copy of the damaged datafile to its state just prior to the failure. This may require all of the archive log files created since the backup in order to recover the restored datafile, which can be quite time-consuming.

![](bbox=[0.05, 0.53, 0.13, 0.59])

# **TIP**

By scheduling frequent backups, the restoration and recovery time can be shortened. The restore time is dependent on the time since the last backup and the amount of data modified since that backup.

By having the latest backup files online as well as the archive log files that had been created since the last backup, you can shorten the time it takes to start the recovery process. By having a plan, and having everything ready to go, things will also run more smoothly.

There are several different ways that the Oracle database can be recovered. These various methods consist of:

+   - Recovery Manager
+       - OS Facilities
+           - Import
+               - Commercially Available Backup Utilities that work with RMAN

Each of these utilities can perform an effective backup. Which of them you use is your own personal preference. However, the preferred method of restore in virtually all cases is via the Recovery Manager.