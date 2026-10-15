
a log file means to divide it into segments by size or by date, keeping several older versions of the log available at all times. Since log rotation is a recurring and regularly scheduled event, it’s an ideal task for cron. See Chapter 11, *Syslog and Log Files* for more details.

## 9.6 EXERCISES

- E9.1  A local user has been abusing his crontab privileges by running expensive tasks at frequent intervals. After asking him to stop several times, you are forced to revoke his privileges. List the steps needed to delete his current crontab and make sure he can’t add a new one.
- E9.2  Think of three tasks (other than those mentioned in this chapter) that might need to be run periodically. Write crontab entries for each task and specify where they should go on your system.
- E9.3  Choose three entries from your system’s crontab files. Decode each one and describe when it runs, what it does, and why you think the entry is needed. (Requires root access.)
- E9.4  Write a script that keeps your startup files (~/. /[a-z]*?) synchronized among all the machines on which you have an account. Schedule this script to run regularly from cron. (Is it safe to blindly copy every file whose name starts with a dot? How will you handle directories? Should files being replaced on the destination machines be backed up before they are overwritten?)

![](img/14d78e3cecac4581d37024baf1e94cca_339_0.png)

We begin this chapter with some general backup philosophy, followed by a discussion of the most commonly used backup devices and media (their strengths, weaknesses, and costs). Next, we talk about how to design a backup scheme and review the mechanics of the popular dump and restore utilities.

We then discuss some additional backup and archiving commands and suggest which commands are best for which situations. Finally, we take a look at Bacula, a free network backup package, and offer some comments about other open source and commercial alternatives.

## 10.1 MOTHERHOOD AND APPLE PIE

Before we get into the meat and potatoes of backups, we want to pass on some general hints that we have learned over time (usually, the hard way). None of these suggestions is an absolute rule, but you will find that the more of them you follow, the smoother your backups and restores will go.

### Perform all backups from a central location

Many backup utilities allow you to perform dumps over the network. Although there is some performance penalty for doing dumps that way, the increase in ease of administration makes it worthwhile. If you manage only a handful of servers, it’s probably easiest to run a script from a central location that executes dump (by way of ssh) on each machine that needs to be dumped. If you have more than a few servers, you should use a software package (commercial or free) to automate this process.

Even if your backups are too large to be funneled through a single server, you should still try to keep your backup system as centralized as possible. Centralization facilitates administration and lets you restore data to alternate servers. Depending on the media you are using, you can often put more than one media device on a server without affecting performance.

Dumps created with dump can only be restored on machines that have the same byte order as the dump host (and in most cases, only on machines running the same OS). You can sometimes use dd to take care of byte swapping problems, but this simple fix won’t resolve differences among incompatible versions of dump.

If you are backing up so much data across a network that the network’s bandwidth becomes an issue, consider creating a LAN dedicated to backup traffic. Many organizations find this approach effective for alleviating network bottlenecks.

### Label your media

Label each piece of backup media clearly and completely—an unlabeled tape is a scratch tape. Directly label each piece of media to uniquely identify its contents. On the cases for the media, write detailed information such as lists of filesystems, backup dates, the format of the backups, the exact syntax of the commands used
