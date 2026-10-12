# Deciding Site Strategy

Whether the tool is a sophisticated backup utility or a simple script, you can automate your backup strategy once you know what it is. Therefore, the first step is to decide what your site strategy will be. As long as what you need is where you can get it when you need it, there are no wrong answers. A site strategy is the list of backup procedures and rules to be followed for this particular site, whether it consists of one machine or 100.

Your backup strategy will consist of answering the following questions:

+   - Which files need to be backed up?
+   - How often do they change, and need re-backing up?
+   - How much storage space will they occupy?
+   - How much storage space is available?
+   - How important are having these files available?
+   - Can you live without these files for any given time period?
+   - How long will it take to go from nothing to usable?

Once you have answered these questions, as only you can do for your system, you will be ready to begin implementing a strategy that fits your needs. This strategy will be your guide to when, how, what, and where to back up your files.

# Types of Backups

There are three basic types of backups, with enough possible variations to handle every contingency. There are full backups, where every file on the computer is saved off to the backup medium. There are partial backups, where only certain files are backed up, typically listed in a file somewhere. Last, but not least, there are incremental backups. Incremental backups deal with the files that have changed since the last backup was done. Each of these has its own advantages and disadvantages, as you will see.

# Full Backups

Traditionally, the term "full backup" was used to describe the process whereby all of the files associated with a particular computer were saved, usually to tape. All that was needed was a full restore to bring the computer back to the state it was in when the full backup was done. The problem with doing a full backup is that it can take a long time, depending on the speed of the backup medium, and it can take up a lot of space on that backup medium. A full backup to a two-gigabyte storage device is not nearly as annoying as trying the same