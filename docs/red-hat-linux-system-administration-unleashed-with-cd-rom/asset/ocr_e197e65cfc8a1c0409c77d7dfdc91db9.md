could significantly reduce the number of restore media needed and the time to complete the restore itself.

If you made a full backup of the original install and have done nothing but incremental backups since, the restoration procedure could take a very long time. In order to minimize this time, you will want to set up a rotation schedule for your backups. Using different levels of backup in such a manner leads to the idea of a rotation schedule. Strangely enough, that's covered next.

# Developing a Rotation Schedule

The term "rotation schedule" refers to the way that information is backed up (using varying levels of incremental backups, usually) and to the number, location, and re-use of your backup media. The backup medium may be tape, tape cartridge, (re)writable CD-ROM, Zip disk, Jaz drive, removable hard drive, floppy disk, or anything else that you want to use. Write-once media can be used for backups, but their reinsertion into the backup pool is not possible. The backup pool is the term used to describe the number of items available (tapes, disks, and so on) for backing up onto.

The purpose of having a rotation schedule is to enable the system administrator (you) to be able to recover specific files with a minimum of effort and wasted time. As an extra side benefit, your users will call you a hero when the deleted file(s) appear back on the system as if by magic. How you let them show their appreciation (read: bribe) is, of course, your concern—and theirs!

How do you decide upon a viable rotation schedule? That depends... are you beginning to hate that phrase? One of the basic criteria will be storage media budget. How much money are you willing to pay during any given time period to protect your data? This will then decide the type of backup medium and the size of your backup pool. How much data needs to be backed up? That data will occupy how many backup media during how long a time period? The following sections illustrate examples of rotation schedules.

# Casual Home User

A simple home system that's used only for email and occasional Web browsing needs to be backed up less often than the system that contains all the financial records for a company. One possible rotation schedule for the typical home user who uses the computer mostly on weekends follows:

+   - Monday: Full (level-0) backup
+   - Tuesday-Friday: Incremental at level-3