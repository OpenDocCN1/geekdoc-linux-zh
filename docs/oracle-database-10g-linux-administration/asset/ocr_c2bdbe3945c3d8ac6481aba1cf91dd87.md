# **Current Online Redo Log Recovery**

Loss of one member of a current online redo log group will not cause the database to cease operations as long as another Oracle-multiplexed member of that group is not affected. Error information is written to the alert log and operation continues.

If all members of a redo log group are lost, you must do a point-in-time restore to the latest archived redo log extended through any redo logs not already overwritten. You can specify both these archived and valid online redo logs during recovery. Recovery from loss of all members of a current online multiplexed redo log group is done by executing a point-in-time recovery.

Mirroring the members of a redo log group to separate disks/controllers is optional, but Oracle strongly recommends operating with each member of a redo log group on separate disks, away from Oracle data files (three members in each group on separate disks under separate controllers, if feasible) to prevent a single point of failure.

# **Inactive Online Redo Log Recovery**

Loss of one member of an inactive online redo log file group will not cause the database to cease operations as long as another multiplexed member of that group is not affected.

You can recover from loss of a single member of an inactive online redo log group as follows:

+   1. If the instance is running, query the v$recovery_file view to find the file needing recovery; otherwise, do a startup, bring the instance to the MOUNT stage, and perform the query.
+   2. Shut down the instance normally.
+   3. Copy the archived log containing the sequence number of the missing/bad redo log to the location of the original redo log.
+   4. Issue the startup command.

You can recover from loss of an entire inactive online redo log group as follows:

+   1. If the instance is running, perform a normal shutdown.
+   2. Start the instance and bring it to the MOUNT stage.
+   3. Query the V$LOG view to ensure the log file has been archived.
+   4. Issue the command ALTER DATABASE CLEAR LOGFILE <file_name> for the bad redo log files. (Use the UNARCHIVED flag if the log file has not been archived.)
+   5. Delete the physical files at the OS level if necessary.