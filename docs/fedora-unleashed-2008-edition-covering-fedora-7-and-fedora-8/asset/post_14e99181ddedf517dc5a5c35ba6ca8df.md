
- **Home user**—At home, the user has the Fedora installation DVD that takes an hour or so to reinstall, so the time issue is not a major concern. The home user should back up any configuration files that have been altered, keep an archive of any files that have been downloaded, and keep an archive of any data files created while using any applications. Unless the home user has a special project in which constant backups are useful, a weekly backup is adequate. The home user is likely to use a DVD-RW drive or other removable media for backups.

- **Small office**—Many small offices tend to use the same strategy as home users, but are more likely to back up critical data daily and use manually changed tape drives. If they have a tape drive with adequate storage, they will likely have a full system backup as well because restoring from the tape is quicker than reinstalling from the CDs. They also might be using CD-RW or DVD writers for backups. Although they will use scripts to automate backups, most of it is probably done by hand.

- **Small enterprise**—Here is where backups begin to require higher-end equipment such as autoloading tape drives with fully automated backups. Commercial backup software usually makes an introduction at this level, but a skilled system administrator on a budget can use one of the basic applications discussed in this chapter. Backups are highly structured and supervised by a dedicated system administrator.

- **Large enterprise**—These are the most likely settings for the use of expensive, proprietary, highly automated backup solutions. At this level, data means money, lost data means lost money, and delays in restoring data means money lost as well. These system administrators know that backups are necessary insurance and plan accordingly.

Does all this mean that enterprise-level backups are better than those done by a home user? Not at all. The "little guy" with Fedora can do just as well as the enterprise operation at the expense of investing more time in the process. By examining the higher-end strategies, you can learn useful concepts that apply across the board.

### NOTE

If you are a new sysadmin, you might be inheriting an existing backup strategy. Take some time to examine it and see whether it meets the current needs of the organization. Think about what backup protection your organization really needs, and determine whether the current strategy meets that need. If it does not, change the strategy. Consider whether users practice the current policy, and, if not, why it is not.

## Backup Levels

Unix uses the concept of backup levels as a shorthand way of referring to how much data is backed up in relation to a previous backup. It works this way:

A level 0 backup is a full backup. The next backup level would be 1. Backups at the other numbered levels back up everything that has changed since the last backup at that level or a numerically higher level (the dump command, for example, offers 10 different backup levels). For example, a level 3 backup followed by a level 4 generates an incremental backup from the full backup, whereas a level 4 followed by a level 3 generates a differential backup between the two.

![](img/34e72348d53ca54c2a1d9c871316691b_304_0.png)

The following sections examine a few of the many strategies in use today. Many strategies are based on these sample schemes; one of them can serve as a foundation for the strategy you construct for your own system.

## Simple Strategy

If you need to back up just a few configuration files and some small data files, copy them to a USB stick, engage the write-protect tab, and keep it someplace safe. If you need just a bit more backup storage capacity, you can copy the important files to a Zip disk (100, 250, and 750MB in size), CD-RW disk (up to 700MB in size), or DVD-RW disk (up to 8GB for data).

In addition to configuration and data files, you should archive each user's home directory, as well as the entire /etc directory. Between the two, that backup would contain most of the important files for a small system. Then you can easily restore this data from the backup media device you have chosen, after a complete reinstall of Fedora, if necessary.

Experts believe that if you have more data than can fit on a floppy disk, you really need a formal backup strategy. Some of those strategies are discussed in the following sections. We use a tape media backup as an example.

## Full Backup on a Periodic Basis

This backup strategy involves a backup of the complete file system on a weekly, biweekly, or other periodic basis. The frequency of the backup depends on the amount of data being backed up, the frequency of changes to the data, and the cost of losing those changes.

This backup strategy is not complicated to perform, and it can be accomplished with the swappable disk drives discussed later in the chapter. If you are connected to a network, it is possible to mirror the data on another machine (preferably offsite); the rsync tool is particularly well suited to this task. Recognize that this does not address the need for archives of the recent state of files; it only presents a snapshot of the system at the time the update is done.

## Full Backups with Incremental Backups

This scheme involves performing a full backup of the entire system once a week, along with a daily incremental backup of only those files that have changed in the previous day, and it begins to resemble what a sysadmin of a medium to large system would traditionally use.

This backup scheme can be advanced in two ways. In one way, each incremental backup can be made with reference to the original full backup. In other words, a level 0 backup is followed by a series of level 1 backups. The benefit of this backup scheme is that a restoration requires only two tapes (the full backup and the most recent incremental backup).

But because it references the full backup, each incremental backup might be large (and grow ever larger) on a heavily used system.

Alternatively, each incremental backup could reference the previous incremental backup. This would be a level 0 backup followed by a level 1, followed by a level 2, and so on. Incremental backups are quicker (less data each time), but require every tape to restore a full system. Again, it is a classic trade-off decision.

Modern commercial backup applications such as Amanda and BRU exist in organizing the process of managing complex backup schedules and tracking backup media. Doing it yourself using the classic dump or employing shell scripts to run tar requires that the system administrator handle all the organization herself. For this reason, complex backup situations are typically handled with commercial software and specialized hardware products that are packaged, sold, and supported by vendors.

## Mirroring Data or RAID Arrays

Given adequate (and often expensive) hardware resources, you can always mirror the data somewhere else, essentially maintaining a real-time copy of your data on hand. This is often a cheap, workable solution if no large amounts of data are involved. The use of RAID arrays (in some of their incarnations—refer to Chapter 35, “Managing the File System,” for more information on RAID) provides for a recovery if a disk fails.

Note that RAID arrays and mirroring systems are just as happy to write corrupt data as valid data. Moreover, if a file is deleted, a RAID array does not save it. RAID arrays are best suited for protecting the current state of a running system, not for providing backups.

## Making the Choice

Only you can decide what is best for your situation. After reading about the backup options in this book, put together some sample backup plans; run through a few likely scenarios and assess the effectiveness of your choice.

In addition to all the other information you have learned about backup strategies, here are a couple of good rules of thumb to remember when making your choice:

- If the backup strategy and policy is too complicated (and this holds true for most security issues), it will eventually be disregarded and fall into disuse.
- The best scheme is often a combination of strategies; use what works.

## Choosing Backup Hardware and Media

Any device that can store data can be used to back it up, but that is like saying that anything with wheels can take you on a cross-country trip. Trying to fit several gigabytes of data on a big stack of CD-RWs is an exercise in frustration, and using an expensive automated tape device to save a single copy of an email is a waste of resources.
