
## Full Backup on a Periodic Basis

This backup strategy involves a backup of the complete file system on a weekly, bi-weekly, or other periodic basis. The frequency of the backup depends on the amount of data being backed up, the frequency of changes to the data, and the cost of losing those changes.

This backup strategy is not complicated to perform, and it can be accomplished with the swappable disk drives discussed later in the chapter. If you are connected to a network, it is possible to mirror the data on another machine (preferably offsite); the rsync tool is particularly well suited to this task. Recognize that this does not address the need for archives of the recent state of files; it only presents a snapshot of the system at the time the update is done.

## Full Backups with Incremental Backups

This scheme involves performing a full backup of the entire system once a week, along with a daily incremental backup of only those files that have changed in the previous day, and it begins to resemble what a sysadmin of a medium to large system would traditionally use.

This backup scheme can be advanced in two ways. In one way, each incremental backup can be made with reference to the original full backup. In other words, a level 0 backup is followed by a series of level 1 backups. The benefit of this backup scheme is that a restoration requires only two tapes (the full backup and the most recent incremental backup). But because it references the full backup, each incremental backup might be large (and grow ever larger) on a heavily used system.

Alternatively, each incremental backup could reference the previous incremental backup. This would be a level 0 backup followed by a level 1, followed by a level 2, and so on. Incremental backups are quicker (less data each time), but require every tape to restore a full system. Again, it is a classic trade-off decision.

You might need to retrieve the version of a file from six days ago or a file that was deleted last week. Such requests from users are not uncommon or unreasonable, and you need to be prepared to meet their needs.

Modern commercial backup applications such as Amanda or BRU assist in organizing the process of managing complex backup schedules and tracking backup media. Doing it yourself using the classic dump or employing shell scripts to run the tar, pax, or cpio applications requires that the system administrator handle all the organization herself. For this reason, complex backup situations are typically handled with commercial software and specialized hardware that are packaged, sold, and supported by vendors.

## Mirroring Data or RAID Arrays

Given adequate (and often expensive) hardware resources, you can always mirror the data somewhere else, essentially maintaining a real-time copy of your data on hand. This is often a cheap, workable solution if no large amounts of data are involved. The use of RAID arrays (in some of their incarnations—see Chapter 37, “Managing the File System,” for more information on RAID) provides for a recovery if a disk fails.

![](img/774d40fd20903495c5cd00e2efad3f33_456_0.png)

Note that RAID arrays and mirroring systems will just as happily write corrupt data as valid data. Moreover, if a file is deleted, a RAID array will not save it. RAID arrays are best suited for protecting the current state of a running system, not for backup needs.

### Making the Choice

Only you can decide what is best for your situation. After reading about the backup options in this book, put together some sample backup plans; run through a few likely scenarios and assess the effectiveness of your choice.

In addition to all the other information you have learned about backup strategies, here are a couple of good rules of thumb to remember when making your choice:

- If the backup strategy and policy is too complicated (and this holds true for most security issues), it will eventually be disregarded and fall into disuse.
- The best scheme is often a combination of strategies; use what works.

### Choosing Backup Hardware and Media

Any device that can store data can be used to back it up, but that is like saying that anything with wheels can take you on a cross-country trip. Trying to fit a gigabyte worth of data on a big stack of 1.4MB floppy disks is an exercise in frustration, and using a $5,000 automated tape device to save a single copy of an email is a waste of resources.

Many people use what hardware they already have for their backup operations. Many consumer-grade workstations have a floppy drive and possibly a CD-RW drive, but they typically do not have the abundant free disk space necessary for performing and storing multiple full backups.

In this section, you learn about some of the most common backup hardware available and how to evaluate its appropriateness for your backup needs. With large storage devices becoming increasingly affordable (160GB IDE drives can be had for around $100) and prices falling on DVD recorders, decisions about backup hardware for the small business and home users has become more interesting.

### Removable Storage Media

At one time, every computer came with a floppy drive, but those drives are becoming less common and are no longer being provided as standard equipment with many new computers. Some sysadmins remove them because they can be used as a means of penetrating system security. (Remember that physical access to a machine means that it is insecure; a floppy drive provides a way to bypass the system administrator to load and run malicious programs.) Many modern laptops do not provide floppy drives except as an option.

Floppy drives are cheap and disposable solutions for making simple, quick backups of a few files by the user, but the media are easily damaged, lost, and accidentally overwritten.

They also unexpectedly fail at times. Floppies now represent the low-rent district for data storage.

### Zip Drives

You can use removable or portable drives as part of your backup strategy. Of all the removable hard drive manufacturers, Iomega seems to have acquired some staying power with its Zip (100, 250, and 750MB) drive. Although these drives have good support in Fedora Core Linux, in the past they have been plagued with mechanical problems that have rendered data irretrievable. Their reliability has improved, but shy away from any older drives. These drives have been ubiquitous and are common in the publishing industry. They are now less frequently encountered and are being supplanting by CD writers.

### USB and Solid-State Drives

USB hard drives and solid-state “pen” drives are the new kids on the block with prices dropping over the last year or two; a 64MB “pen” drive costs slightly less than $30 and capacities up to 1GB are available for around $90. USB drives have a large capacity for their size. If your machine supports them (or if you have purchased a card reader), you can also use Compact Flash devices, which come in sizes up to 8GB in the Flash memory versions and 4GB for Hitachi Microdrives. Both USB hard drives and solid-state drives are highly portable. Support for these drives under Fedora Core Linux is very good, accommodating these drives by emulating them as SCSI drives—the system usually sees them as /dev/scd1. Watch for improved support and ever falling prices in the future. The newer USB 2.0 hard drives are significantly faster than the older USB 1.0 hard drives. A 100GB USB hard drive will cost about $150. The biggest benefits of USB drives are data transfer speed and portability.

### FireWire Drives

FireWire (IEEE-1394) hard drives are similar to USB drives; they just use a different interface to your computer. Many digital cameras and portable MP3 players use FireWire. Kernel support is available if you have this hardware; a 100GB FireWire drive will cost about $180, roughly twice IDE drive prices. Found mostly on the Mac, controller and drive hardware exists for the PC platform as well.

### CD-RW and DVD+RW/-RW Drives

Compared to floppy drives and some removable drives, CD-RW drives and their cousins, DVD+RW/-RW drives, can store large amounts of data and are useful for a home or small business. Once very expensive, CD writers and media are at commodity prices today, although automated CD changing machines, necessary for automatically backing up large amounts of data, are still quite costly. A benefit of CD and DVD storage over tape devices is that the archived uncompressed file system can be mounted and its files accessed randomly just like a hard drive (you do this when you mount a data CD, refer to Chapter 10, “Multimedia Applications”), making the recovery of individual files easier.

Each CD-RW disk can hold 650MB–700MB of data (the media comes in both capacities at roughly the same cost); larger chunks of data can be split to fit on multiple disks. Some backup programs support this method of storage. Once burned and verified, the shelf life
