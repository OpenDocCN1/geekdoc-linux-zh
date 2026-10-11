is the same as a full backup, except only part of the filesystem is backed up instead of the entire system.

The advantage of doing a differential backup is that it is faster than doing a full backup. Also, because the total size of the files you are backing up is smaller, the backup is more likely to not require you to change the media.

The disadvantage of performing differential backups comes into play when you have to perform a restore. It will take you longer to restore when you use differential backups than if you use only full backups.

If you are restoring your entire system, you will need to restore the last full backup followed by any differential backups that have been performed since that time. These must be applied in the same order that they were made. Also, if you are restoring a file for a user, you might have to look through several differential backups before you find the desired file.

> > **Key Concept**
> > Four different types of backups exist. They are *copy*, *full*, *partial*, and *differential* or *incremental*.

# How Long Should You Keep Backups?

Often you will be requested to restore a file that was deleted by mistake. Because these types of errors are not usually discovered immediately, the backup containing the file could be a week or more old.

When planning your backup strategy, you should consider how vital your information is and how frequently it is accessed. Use this information to decide how frequently you should recycle the reusable media you are using for backups.

For example, you might want to save your backups for a minimum of eight weeks. That means you should have enough media to hold eight weeks of backups. After eight weeks, you can recycle the oldest tape or disk. In addition, you might want to archive a full backup once a month and keep it for a year or more. Your organization's business model and the type of information you are backing up are integral to making this decision. One possible backup strategy might be

+   1.  Full backup every Friday; reuse this tape in nine weeks
+   2.  Differential backup every Monday through Thursday; reuse these tapes in nine weeks
+   3.  Archive the first full backup of every month by placing it in the vault and keep it for one year