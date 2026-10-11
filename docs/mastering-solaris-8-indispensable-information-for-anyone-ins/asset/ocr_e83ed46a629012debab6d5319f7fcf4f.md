stored on tape compared to disk per unit cost is even better. There are some in the industry who feel that the cost of backing up to disk will eventually be lower than the cost of backing up to tape, but that possibility still seems several years out; at the moment, the great preponderance of backup information is written to tape drives and tape libraries.

> **NOTE** For information about working with and installing tape drives, see Chapter 6.

# ### Backup Strategies

Most thorough administrators use a system of rotating and saved backups. The question really isn't whether you should back up, but how often. The answer to that question is determined by variables such as these:

+   * The length of your backup window
+   * The length of your restore window
+   * The rate at which your data is changing
+   * The amount of data you can afford to lose if a critical system fails
+   * The amount of historical data you need to store

Before you can decide what particular type of backup strategy you need to employ, you need to know what these variables are. It's important to note that they are dependent upon hardware and software configurations, as well as on business conditions that are likely to change. For a stand-alone system, your backup strategy can be used for quite some time. In an enterprise, administrators should periodically revisit their backup strategy from time to time.

Although it might be desirable to do one or two full backups a day, it isn't often practical to do so. Most system administrators do periodic full backups with multiple incremental backups in between. When you apply that system, you need to perform a full backup and then apply all of the incremental backups that occurred since the last time you backed up fully in order to fully restore a system. The more incremental backups you do, the more time you save backing up your system but the more time you spend restoring it. It's a compromise of time versus materials.

There are actually two different types of incremental backups possible: an incremental backup to the last full backup and an incremental backup to a previous incremental