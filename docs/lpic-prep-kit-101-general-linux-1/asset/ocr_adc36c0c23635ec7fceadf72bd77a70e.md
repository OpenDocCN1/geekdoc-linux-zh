However, it is a good idea to periodically back up system and application files. Having a recent backup will enable you to bring your system back up with all the latest patches already applied in a shorter period of time.

For data files, you can have databases or other files that seldom change but can be used to retrieve information on a regular basis. In addition, some files change on an almost daily basis.

If you organize your files based on the frequency with which they change, it will be much easier to plan your backup strategy. See Chapter 6, “Maintaining the Filesystem,” for more information on the Linux filesystem hierarchy and organizing your files.

Putting volatile data on separate partitions is another way to simplify your disaster recovery plans. If all your users’ home directories are on a separate partition, you easily can back up this partition on a daily basis.

# Backup Frequency

After you have decided on what files you want to back up—and chances are you decided on backing up everything—you will need to decide how frequently to back them up. You do not need to back up every file every day, although you could.

If files do not change, such as system and application files, why should you go to the expense of backing them up every day? Instead, you can elect to back them up weekly or monthly. Of course, you will want to back them up whenever you upgrade or make configuration changes. You also will want to perform a periodic backup of these files to ensure that you have a valid backup that can be used if you ever have to restore your system.

For files that change frequently, ask yourself the following question. What is the cost to my organization if that data is lost before a backup is performed? In most situations, daily backups of changing files is adequate. However, if you have mission-critical information that changes hourly, you might want to back up these files more frequently.

# How Much Time Do You Have to Run Your Backup?

When planning what to back up, you will need to consider the amount of time you have for running the backup and how long it will take to back up the selected files.

For high availability systems, you might have a narrow window when certain files are available for backing up. Plan your backups appropriately. Even if you have to back up a few files at a time, you still should back up as frequently as you can.

# Media Selection

Next, you will need to consider where to save your backups. Traditionally, this has been a tape drive. The advantages of using a tape drive include that they are relatively inexpensive—both the tape unit itself and the tapes. In addition, it is a technology that is well-known and very reliable.