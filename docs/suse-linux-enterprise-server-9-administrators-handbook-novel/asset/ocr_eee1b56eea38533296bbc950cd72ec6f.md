# TIP

If you have a corrupted lilo boot loader, boot your system using the rescue disk and then reinstall lilo on the MBR of your hard disk using the /sbin/lilo -M command.

# A Look at Backup Strategies

The purpose of performing backups is to be able to restore individual files or complete filesystems. How often to perform backups, what data should be backed up, and how to rotate backup media are issues that can be confusing.

Exactly how often you should back up which files depends on your system hardware configuration and particular needs. The criterion is, “If the system crashes, how much work are you willing to lose, and how much data can you afford to lose?” Remember that in any computing environment, the most valuable component is data, which may be in the form of databases or source code. Ideally, you would want to back up all files on all filesystems every few minutes so that you would never lose more than a few minutes’ worth of work. However, this approach is not practical, and there are other ways in which you can achieve this near real-time redundancy without doing backups.

# TIP

One option to achieve (near) real-time redundancy, without installing special hardware, is to periodically mirror the data from your server to a backup server using rsync, a file-synchronization utility included with SLES. rsync is discussed later in this chapter.

To examine the problem another way, you might ask this question: “How often should I back up the files?” The more users you have on the system, the more often you should back up the filesystems. A common schedule is to perform a full backup once or twice a week and partial daily backups. In a full backup, every single file on every filesystem is backed up, regardless of its creation or modification time. A partial, or incremental, backup backs up only the files that have been created or modified since the last full backup.

Your backup strategy should be based on a rotation scheme that guarantees complete recovery in case of a disaster, within a reasonable amount of time. The following discussion is based on tape rotation because the most commonly used backup medium today is tape; however, the same principle applies to other storage media, such as rewritable DVDs.