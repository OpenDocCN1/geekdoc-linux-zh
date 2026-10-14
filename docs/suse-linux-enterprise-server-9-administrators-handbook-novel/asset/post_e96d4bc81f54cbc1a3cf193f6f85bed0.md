
## FIGURE 9.8
The Administration menu for the CUPS web interface.

![](img/ae8469257d2662b469f2360b3bbbe322_341_0.png)

The Class page is shown in Figure 9.9. As with subsequent administration pages, the Delete and Modify options are shown. Access to these selections requires appropriate authentication. Unauthorized users are simply presented with an authorization failure (an HTTP 403 error).

## FIGURE 9.9
The CUPS Class page.

![](img/ae8469257d2662b469f2360b3bbbe322_341_1.png)

Figures 9.10 and 9.11 complete the series of menu options available under the CUPS web interface. Within the Jobs page, shown in Figure 9.10, you can see information on pending print jobs. Similarly, the Printer page, shown in Figure 9.11, presents configuration information on each printer, status information, as well as a number of management options.

## FIGURE 9.10
The CUPS Jobs management page.

![](img/ae8469257d2662b469f2360b3bbbe322_342_0.png)

## FIGURE 9.11
The CUPS Printer management page.

![](img/ae8469257d2662b469f2360b3bbbe322_342_1.png)

The CUPS web interface into printer configuration management is an important step in easing the support of a distributed printing environment. The CUPS environment incorporates its own administration model. This permits the granting of administration rights to individuals outside the authentication scheme of the hosting server. Users who do not possess any privileges on the host server can therefore be granted administration rights directly within CUPS. This adds an additional layer of administrative burden when implementing an account management policy. It does, however, allow for the delegation of queue management to individuals such as helpdesk staff without the requirement of elevated user privileges on the server.

## Summary

In this chapter, we examined the different aspects of printing. SLES provides for a number of different methods for creating and maintaining queues.

Using YaST, we created both a local and a network print queue. We used command-line tools to fine-tune characteristics of these queues and submit jobs.

Throughout this chapter, we saw how the CUPS printing environment has made queue management simpler. Additionally, we examined how the CUPS web interface can be used to remotely manage the printing environment without requiring local access to the print server itself.

## Data Backup and Disaster Recovery

No matter how fault tolerant your server hardware is or if you have implemented the best security measures possible, there is no guarantee that data will never be lost. Sometimes the cause is totally beyond your control—fire caused by a gas leak, for example, or even Mother Nature (remember the Los Angeles earthquake?). Also, to err is human; even the most experienced users and system administrators make mistakes. Deleting the wrong file or mistyping information into a file (such as `/etc/passwd`) can cause unwarranted headaches and additional work for yourself or coworkers who need to access the data, or, in the worst case, the deletion renders the whole system unusable. Also, a disgruntled user or malevolent hacker may deliberately remove or corrupt essential data or system files; as a matter of fact, most attacks occur from within the company rather than from without. In all cases, having up-to-date backups would be a lifesaver.

Recovering from a hacker break-in can be tedious work. The problem is that once a system has been compromised, it is essentially impossible to determine everything that has occurred, especially if the system's root account has been compromised. Log files and audit trails help, but if the hacker covered his or her tracks well, there will be no telltale signs found. So the best way to quickly recover from any break-in is to use a pristine backup.

To be able to use such a backup, it is of utmost importance that you have developed and implemented a reliable data backup and disaster recovery strategy. In this chapter, you learn how to develop a backup plan and how and when to use the standard Linux backup tools, such as tar and cpio. You also find out how to create and use an SLES rescue floppy disk using YaST.

### TIP

If you have a corrupted lilo boot loader, boot your system using the rescue disk and then reinstall lilo on the MBR of your hard disk using the /sbin/lilo -M command.

## A Look at Backup Strategies

The purpose of performing backups is to be able to restore individual files or complete filesystems. How often to perform backups, what data should be backed up, and how to rotate backup media are issues that can be confusing.

Exactly how often you should back up which files depends on your system hardware configuration and particular needs. The criterion is, “If the system crashes, how much work are you willing to lose, and how much data can you afford to lose?” Remember that in any computing environment, the most valuable component is data, which may be in the form of databases or source code. Ideally, you would want to back up all files on all filesystems every few minutes so that you would never lose more than a few minutes’ worth of work. However, this approach is not practical, and there are other ways in which you can achieve this near real-time redundancy without doing backups.

### TIP

One option to achieve (near) real-time redundancy, without installing special hardware, is to periodically mirror the data from your server to a backup server using rsync, a file-synchronization utility included with SLES. rsync is discussed later in this chapter.

To examine the problem another way, you might ask this question: “How often should I back up the files?” The more users you have on the system, the more often you should back up the filesystems. A common schedule is to perform a full backup once or twice a week and partial daily backups. In a full backup, every single file on every filesystem is backed up, regardless of its creation or modification time. A partial, or incremental, backup backs up only the files that have been created or modified since the last full backup.

Your backup strategy should be based on a rotation scheme that guarantees complete recovery in case of a disaster, within a reasonable amount of time. The following discussion is based on tape rotation because the most commonly used backup medium today is tape; however, the same principle applies to other storage media, such as rewritable DVDs.

A rotation system distributes both old and new information across several tapes to reduce the risk of being lost due to media failure. The backup and storage media type and media rotation method you choose should take the following into consideration:

- **Backup time window**—How much of a time window do you have when files on the servers are not being updated? Unless your backup software is capable of backing up open files, you need to schedule the job for the time period when no files are being accessed, or you have to make a conscious decision to skip opened files.

- **Amount of data and backup media throughput**—Both the amount of data to back up and the speed at which that data can be written to the backup media will have an impact on your choice of backup methods. For example, if you have 20GB of data to be backed up daily and your backup device is capable of storing only 1GB per hour, performing a full backup will take at least 20 hours. In such a case, doing a daily full backup is probably not a good option, and a daily incremental backup is more appropriate.

- **Media reliability and capacity**—Tapes have a limited lifetime, and constant use of the same tape can shorten its life span. The typical shelf life of a magnetic tape is just a few years, or shortened depending on the environment in which it is stored. On the other hand, tapes have a much higher storage capacity (hundreds of gigabytes) than most other storage media, such as CDs (800MB) and DVDs (4–8GB). Some installations use tapes for short-term storage, and when certain data needs to be retained for an extended period of time, this data is transferred to DVDs. In some cases due to audit requirements, data is backed up directly to CDs or DVDs so they cannot be subsequently modified.

- **File restoration decision**—How many tapes (that is, how much time) will you need to restore information in the event of a complete system failure? (Always plan for the worst-case scenario, but hope for the best.) Also, the procedure to restore your filesystems back to a known state (for example, last night) should be as straightforward as possible; you should not have to run through 20 tapes for the task.

- **Storage facilities**—It is general practice that backup archives should be sent to offsite storage facilities for safe-keeping. However, this may not be feasible in all cases, especially with smaller companies. In such instances, you need to consider the question “How many tapes are you physically capable of storing safely and securely onsite?” For instance, your backup tapes should be locked in a fire-resistant safe (one especially designed for tapes and magnetic storage media, and not one for documents). That
