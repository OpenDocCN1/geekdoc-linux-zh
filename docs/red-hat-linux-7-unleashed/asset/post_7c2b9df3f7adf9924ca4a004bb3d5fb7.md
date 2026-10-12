
- comp.os.linux.m68k
- comp.os.linux.misc
- comp.os.linux.networking
- comp.os.linux.portable
- comp.os.linux.powerpc
- comp.os.linux.questions
- comp.os.linux.setup
- comp.os.linux.x

The preceding list consists of just a few of the actual newsgroups that specifically deal with Linux. Most of the others are similar to those listed. It is probably best to scan the newsgroups that you have access to for Linux.

### Tip

There is a tool out there on the Web by deja.com that allows you to search the newsgroups. It's very helpful because most likely someone else has already asked your question. Go to http://www.deja.com/usesnet.

In addition to newsgroups, myriad Web pages are devoted to Linux—Red Hat specifically. When I performed a search on WebCrawler (http://www.webcrawler.com) for Linux, the search located 17,789 documents; searching on Linux AND Redhat, the search located 2640 documents. Considering so many choices and the volatility of the Web, it might be helpful if I point out and briefly describe a few Web resources I believe will be around for a while.

The first one, which should be obvious, is Red Hat’s home page at http://www.redhat.com. It is, of course, the first place to look for any information concerning Red Hat Linux. Also, for general Linux information, good places to start are http://www.linux.com and http://www.linux.org.

Another great source for information about Linux (as well as every other type of UNIX) is http://www.uguu.com, the UNIX Guru Universe page. According to the site’s front page, it is “the largest single point UNIX resource on the Net!” This Web site is highly configurable and provides a great deal of information on everything of value to the UNIX community.

The Linux Documentation Project (http://www.linuxdoc.org) has a tremendous number of links, providing everything from general Linux information, to Linux user groups, to Linux development projects. Although I do not think there is much, if anything, unique about this site, it is complete. It has information on just about everything associated with Linux including a large library of HOWTOs to help you do everything from configuring an NFS server to hacking the Linux kernel.

## Summary

This chapter gave you a glimpse into the world of system administration. Some of the material presented in this chapter may be overkill for somebody administering only a few users. For those administering a large system, the responsibilities are far greater. However, all system administrators need to understand the basics for managing software, managing users, and making sure their system is secure.

## CHAPTER 22

# Backup and Restore

### IN THIS CHAPTER

- Successful Backup Considerations 738
- Qualities of a Good Backup 738
- Selecting a Backup Medium 739
- Selecting a Backup Tool 740
- Backup Strategies and Operations 742
- Restoring Files 747
- What Is in the Archive? 747

Depending on how you put Red Hat Linux to work, your system or systems can quickly acquire enormous amounts of valuable data. Data can be in the form of text documents, spreadsheets, graphics, software programs, databases, or numerous large or small files. Data is important because of the time it takes to create it. Even a customized Red Hat Linux system tailored for your computer and peripherals can take time to re-create. If you run a multiuser system, anywhere from 2 to 200 to 2,000 users will depend on you to safeguard their data.

Data can be lost by operator error, bad software, hardware failure, malicious cracking, or natural disaster, but savvy system administrators will devise efficient and inexpensive ways to prevent this. This chapter touches on some basic concepts to keep in mind, and introduces a few software tools included with your Red Hat Linux system that you can use to back up or restore data.

You'll learn about the qualities of a good backup plan, see the process for selecting a reliable backup medium or tool, and learn about different backup strategies.

### Successful Backup Considerations

Backups can protect your investment in time and in data, but only if you are successful in backing up and keeping the information; therefore, part of a successful backup procedure is a test strategy to spot-check backups. The easiest way to spot-check your backups is to perform a restore with them, which you should attempt before it is actually needed.

If you automate the backup process, such as through the use of crontab scripts, make sure to perform extensive test runs in parallel with sure techniques before relying on automation.

### The Difference Between Backup and Archive

You need to understand the difference between a backup and an archive. A good backup strategy involves both forms of data protection. Backups are file operations that save your data at regular intervals, either wholly or incrementally (see “Backup Strategies and Operations,” later in this chapter). Archives are file operations that save your data for long periods of time. For example, the CD-ROM included with this book is an archive of the free portions of the latest Red Hat Linux distribution.

### Qualities of a Good Backup

Obviously, in the best of all possible worlds, backups would be perfectly reliable, always available, easy to use, and really fast. In the real world, trade-offs must be made. For example, backups stored offsite are good for disaster recovery, but are not always available.

Above all, backups need to be reliable. A reliable backup medium will last for several years, whereas a reliable archive medium should last much longer. Of course, if the backups are never successfully written to the backup medium, it does not matter how good the medium is, and today’s ever-increasing storage requirements can tax even the very best hardware and strategies.

Speed is more or less important, depending on the system and use of the data. If a time window is available when the system is not being used and the backup can be automated, speed is not an issue. On the other hand, restoration might be an issue. The time it takes to restore the data is as important as the need to have the data available.

Availability is a necessary quality. Performing regular backups does no good if, when they are needed, they are unavailable. Backups for disaster recovery may not be available locally and don’t always include data timely enough to restore a single file accidentally deleted by a user. A good backup and recovery scheme includes both a local set of backups for day-to-day restores and an offsite set of backups for disaster recovery purposes.

Fast, available, reliable backups are no good if they are not usable. The tools used for backup and restoration need to be easy to use. This is especially important for restoration. In an emergency, the person who normally performs the backup and restores might be unavailable, and a nontechnical user might have to perform the restoration. Obviously, documentation is a part of usability.

### Selecting a Backup Medium

Today, many choices of backup media exist, although the three most common types for a long time were floppy disks, tapes, and hard drives. Table 22.1 rates these media—and newer ones such as CD-ROM read-only and CD-RW—in terms of reliability, speed, availability, and usability.

**TABLE 22.1 Backup Media Comparison**

| Medium | Reliability | Speed | Availability | Usability |
| :--- | :--- | :--- | :--- | :--- |
| Floppy disks | Good | Slow | High | Good with small amounts of data; bad with large amounts of data |
| CD-ROM RO | Good | Medium | High | Read-only media; okay for archives |
| CD-RW | Good | Medium | Medium | Read-write media; economical for medium-sized systems |
| DVD | Good | Slow | Low | Expensive |
| Iomega Zip | Good | Slow | High | 100-250MB storage; okay for small systems |
| Flash ROM | Excellent | Fast | Low | Very expensive; currently limited to less than 1GB |
| Tapes | Good | Medium/Fast | High | Depending on the size of the tape, can be highly usable; tapes cannot be formatted under Linux |
| Removable HD | Excellent | Fast | High | Relatively expensive, but available in sizes of 2GB or larger |
| Hard drives | Excellent | Fast | High | Highly usable |

Writable CDs are good for archival purposes, and some formats, such as CD-RW, can be overwritten nearly 1,000 times; however, the expense in time tends to be high if a large number of regular archives or backups must be made. Flopticals, with attributes of both floppy and optical disks, tend to have the good qualities of floppy disks and tapes and are good for single file restoration. Flopticals can hold a lot of data, but have not captured the consumer market; they are popular in high-end, large-scale computing operations. More popular removable-media are Iomega Zip and Jaz drives, which come in 100MB and 250MB Zip and 1-2GB Jaz form factors. Digital DAT tapes can hold many gigabytes of data, and are also popular.

### Selecting a Backup Tool

Many tools are available for making backups. In addition to numerous third-party applications, Red Hat Linux comes with some standard tools for performing this task. This section examines two of them, tar and cpio.

tar and cpio are very similar. Both are capable of storing and retrieving data from almost any media. In addition, both tar and cpio are ideal for small systems, which Red Hat Linux systems often are. For example, the following tar command saves all files under /home to the standard output (which can then be redirected to your system's backup device or directory):
