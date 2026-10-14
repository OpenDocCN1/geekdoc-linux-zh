# A Linux Backup Strategy

Different backup strategies balance the desire for a complete backup of data at all times with the need for convenience in creating and maintaining backups. The method described here is a standard used for many Linux and UNIX systems. You can adjust the time frames according to how often the data on your system changes.

# Using Backup Levels

This strategy relies on multiple backup levels. A backup level defines how much data is to be backed up in comparison to another backup level. A backup operation at a given backup level stores all of the data that has changed since the last backup of the previous level. For example, a backup at level one stores all files that have changed since the last level zero backup; a backup at level two stores all files that have changed since the last level one backup. A commonly used arrangement operates with three levels, as described here:

+   - Level zero is a full backup (also called an epoch backup). Everything on the system is backed up. A level zero backup might be performed on the first of every month.

+   - A level one backup might be done once per week. Every file that has been modified since the last level zero backup (on the first of the month) is included in the level one backup. Storing only files that have changed since a full backup is called a differential backup.

+   - A level two backup could then be done each day. Every file that has been modified since the first of the week (the last level one backup) is included in the level two backup. This is also considered a differential backup.

Figure 13-1 illustrates the three-level backup just described.

![](bbox=[0.15, 0.82, 0.75, 0.94])

Figure 13-1 Backup levels

Another important backup term is incremental backup. The difference between a differential backup and an incremental backup can be confusing in this multilevel scheme. A differential backup stores all files that have been changed since the most recent full backup. An incremental backup only stores files that have been changed since the most