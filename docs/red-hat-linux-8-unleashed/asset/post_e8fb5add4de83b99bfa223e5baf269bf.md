
## CHAPTER 11 Backing Up, Restoring, Recovery

It’s a good idea to examine incidents of data loss in the past and decide if your chosen scheme will adequately address that loss. Finally, examine what effect a total disaster might have. In each case, ask yourself: What data am I protecting? Will it be safe? How will it be restored, and how long will it take? The answers to all these questions should help you form your plan.

To formulate your backup plan, you need to determine the frequency of backups. The necessary frequency of backups should be determined by how quickly the important data on your system changes. On a home system, most files never change, a few change daily, and some weekly. No elaborate strategy needs to be created to deal with that. A good strategy for home use is to back up (any kind of removable media) critical data frequently and back up configuration and other files.

At the enterprise level on a larger system with multiple users, a different approach is called for. Some critical data is changing constantly, and it could be expensive to recreate; this typically involves elaborate strategies between these extremes. Assess your system and use it to determine where you fall in this spectrum.

Backup schemes and hardware can be elaborate or simple, but they all require a workable plan and faithful follow-through. Even the best backup plan is useless if the process isn’t carried out, data isn’t verified, and data restoration isn’t practiced on a regular basis. Whatever backup scheme you choose, you should incorporate in these three principles:

- Have a Plan—Design a plan that is right for your needs and have equipment appropriate to the task. This involves assessing all the factors that affect the data you’re backing up. We’ll get into more detail later in the chapter.
- Follow the Plan—Faithfully complete each part of your backup strategy, and then verify the data stored in the backups. Backups with corrupt data are of no use to anyone. Even backup operations can go wrong.
- Practice Your Skills—Practice restoring data from your backup systems, so when the time comes, you’re ready (and able) to benefit from the strength of your backup plan. (For restoring data, see the section titled “Using Backup Software.”)

> NOTE
If you are a system administrator serving other users (as opposed to being both the system administrator and the sole user), your insistence on following system policies and adhering to backup procedures might make you the object of cruel jokes or you to be shunned at the annual office party. However, when you recover a file for those same people, you will become their best friend (for the moment, least).

## Practices

You have to create your own best-backup plan, but here are some building blocks that you can put into the foundation of any sound backup program:

- Maintain more than one copy of critical data.
- Label the backups.
- Store the backups in a climate-controlled and secure area.
- Use secure, off-site storage of critical data.
- Establish a backup policy that makes sense and can be followed religiously.
- Routinely verify backups and practice restoring from them.
- Routinely inspect backup media for defects and regularly replace them (after destroying the data on them if it is sensitive).

## Evaluating Backup Strategies

Now that you've decided backups, you need a strategy. It's difficult to be specific because each user or administrator's strategy will be highly individualized, but here are a few general examples:

- Home User—At home, the user has the Red Hat installation CDs that can take an hour or more to re-install, so the time is not a major concern. The home user will want to back up any configuration files that have been altered, keep an archive of any files that have been created while using any applications. Unless the home user has a special project (like writing this book) in which constant backups are useful, a weekly backup is adequate. The home user will likely use a floppy disk, CD-RW drive, or other removable media for backups.
- Small Office—Many small offices use the same strategy as the Home User, but are more likely to back up critical data and use changed tape drives. If they use a tape drive with adequate storage, they will likely have a full system backup when restoring from the tape is quicker than re-installing the CDs. They also might be using CD-RW or DVD writers for backups. Although they will use scripts to automate backups, it is probably done by hand.
- Small Enterprise—Here backups begin to require higher-end equipment like auto-loading tape drives with fully automated backups. Commercial backup software usually makes an introduction at this level, but a skillful system administrator on a budget can use one of the basic applications discussed in this chapter. Backups are highly structured and supervised by a dedicated system administrator.
- Large Enterprise—These are the most likely settings for the use of expensive, proprietary, highly automated backup solutions. At this level, data means money lost, and delays in restoring data means money lost as well. System administrators know that backups are nothing more than necessary insurance and plan accordingly.

## CHAPTER 11 Backing Up, Restoring, and Recovery

Does all this mean that Enterprise-level backups are better than done by a Home User? Not at all. The “little guy” with Red Hat Linux can do just as well as the Enterprise operation at the expense of investing more time in the process. By examining the higher-end strategies, we can apply useful concepts across the board.

> NOTE
If you are a new sysadmin, you might be inheriting an existing strategy. Examine and see if it meets the current needs of the organization. Think about what is really needed, and determine if the current strategy meets that. If it doesn't, change it. Consider whether the current policy is being practiced by the users, and, if not, why it is not.

## Backup Levels

UNIX uses the concept of backup levels as a shorthand for referring to how much data is backed up in relation to a previous backup. It works this way:

A level 0 backup is a full backup.

Backups at the other numbered levels will back up everything that has changed since the last backup at that or a numerically higher level (the dump command, for example, offers 10 different levels). For example, a level 4 will generate an incremental backup from the full backup, whereas a level 4 followed by a level 3 will generate a differential backup between the two.

The following sections examine a few of the many strategies in use today. Many strategies are based on these sample schemes; one of them can serve as a foundation for the strategy you construct for your own system.

## Simple Strategy

If you need to back up just a few configuration files

In addition to configuration and data files, you should archive each user’s home directory, as well as the entire /etc directory. Between the two, that backup would contain most of the important files for a small system. Then, you can easily restore this data from the backup media you’ve chosen, after a complete reinstall of Red Hat. We believe that if you’ve got more data can fit on a floppy disk, you really need a formal strategy. Some of those are discussed in the following sections. We use tape media as an example.

## Full Backup on Periodic Basis

This backup strategy involves a backup of the complete filesystem on a weekly, bi-weekly, or other periodic basis. The frequency of the backup depends on the amount of data backed up, the frequency of changes, and the cost of losing those changes. This backup strategy isn't complicated to perform, and it can be accomplished with swappable disk drives. If you are connected to a network, it is possible to mirror the data to another machine (preferably off-site); the rsync tool is particularly well suited to this task. Recognize that this doesn't address the need for archives of the current state of files the update is done.

This scheme performs a full backup of the entire system once a week, along with a daily incremental backup of only those files that have changed in the previous day, and it begins to resemble what a sysadmin of a medium to large system would traditionally use.

In one way, each incremental backup can be made with reference to the full backup. In other words, a level 0 backup is followed by a series of level 1 backups. The benefit of this backup scheme is that a restoration requires only two tapes (the full backup and the most recent incremental backup). Because it references the full backup, each incremental backup might be large (and grow larger) on a heavily used system.

## Full Backups with Incremental Backups

Alternatively, each incremental backup could reference the previous incremental backup. This would be a level 0 backup followed by a level 1, followed by a level 2, and so on. Backups are quicker (less data each time), but require each tape to restore a full system. It is a classic trade-off decision. You might need to retrieve the version of a file from six days ago or a file that was deleted last week. Such requests from users are not uncommon or unreasonable, and you need to be prepared to meet their needs. In these situations, you require a more elaborate scheme that uses multiple sets of media so that the archives reach each server backup.

## Daily Backups with Rotating Media

Many administrators use this scheme because it's simple. It's also incredibly shortsighted and likely a waste of time. In the nightmare version of this scheme, one tape is left in the machine, and a script performs the backups every day or so. At no time is anyone verifying that the backed up data is good and can be restored, so if the backup fails in any way, data is retrievably lost and can continue to be lost until someone attempts to restore operation and discovers the problem.

Many sysadmin has been lulled into a false sense of confidence with this scheme. The best you might say is that it is better than nothing, but even that it's wrong: Regular users
