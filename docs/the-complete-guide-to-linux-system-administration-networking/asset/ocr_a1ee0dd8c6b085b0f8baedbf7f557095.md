If a file was created and deleted on the same day, it wouldn’t be part of any backup plan that backed up data each evening. If a user asks for help in this situation, you would need to rely on undelete utilities to find the deleted file on the hard disk. Examples of these utilities include e2undel, R-Linux (see www.r-tt.com), and recover.

# Advantages to the three-level backup method include:

+   - Creating the level two daily backups requires little of the system administrator’s time because few files are altered on any given day.
+   - No user ever loses more than a single day’s work because the changes in the file system from each day are recorded in a level two backup.
+   - Files that rarely change are still backed up and available, but don’t require daily maintenance by the system administrator.

Some backup utilities explicitly use the term "backup levels" to refer to how data is backed up and how backup media are tracked. The concept can be applied to any backup utility, however. For the system to work well, you need to keep careful records and label backup media clearly.

In the event that an entire system must be restored using a set of backup media that have been prepared using the three-level method, a system administrator would follow this procedure:

+   1. Restore everything from the most recent level zero backup.
+   2. Restore everything from the most recent level one backup.
+   3. Restore everything from the most recent level two backup.

Figure 13-2 illustrates how this procedure results in all of the latest information being included in the restored file system. (Compare the backup levels pictured in Figure 13-1 to the restore operation pictured in Figure 13-2.)

![](bbox=[0.18, 0.75, 0.45, 0.93])

# Figure 13-2 Restoring data from a three-level set of backup media