
## Selecting a Backup Strategy

While it is tempting to do the quick-and-easy backup, backing up important data requires more planning and forethought. There are several approaches you can take to backing up your data. You need to ask yourself a few questions to decide which approach is best for you. Some things that you should consider are:

- In the event of a crash, how much downtime can I tolerate?
- Will I need to recover older versions of my files or is the most recent revision sufficient?
- Do I need to back up files for just one computer or for many computers on a network?

Your answers to these questions will help you decide how often to do full backups and how often to do incremental backups. If the data is particularly critical, you may even decide that you need to have your data duplicated constantly, using a technique called disk mirroring. The following sections describe different backup methods.

### Full backup

A full backup is one that stores every file on a particular disk or partition. If that disk should ever crash, you can rebuild your system by restoring the entire backup to a new disk. Whatever backup strategy you decide on, some sort of full backup should be part of it. You may perform full backups every night or perhaps only once every week; it depends on how often you add or modify files on your system, as well as the capacity of your backup equipment.

### Incremental backup

An incremental backup is one that contains only those files that have been added or modified since the last time a more complete backup was performed. You may choose to do incremental backups to conserve your backup media.

Incremental backups also take less time to complete, because they only back up data that has changed since the most recent backup (full or incremental). Incremental and other partial backup types can be important when systems are in high use during the workweek and running a full backup would degrade system performance. Full backups can be reserved for the weekend when the system is not in use.

### Disk mirroring

Full and incremental backups can take time to restore, and sometimes you just can't afford that downtime. By duplicating your operating system and data on an additional hard drive, you can greatly increase the speed with which you can recover from a server crash.

With disk mirroring, it is usually common for the system to continuously update the duplicate drive with the most current information. In fact, with a type of mirroring called RAID 1 (described in Chapter 10), the duplicate drive is written to at the same time as the original, and if the main drive fails, the duplicate can immediately take over. This is called *fault-tolerant* behavior, which is a must if you are running a mission-critical server of some kind.

You can tailor different RAID levels to use features other than mirroring. Other RAID levels use striping and can be tuned for performance, data redundancy, and cost. Software RAID is supported in the Linux kernel and several hardware vendors have RAID controller cards for SATA, IDE, and SCSI disk configurations that work well in Linux. Vendors include LSI Logic (www.lsilogic.com), Promise (www.promise.com), and 3Ware (www.3ware.com). See http://tldp.org/HOWTO/Software-RAID-HOWTO.html for further information on RAID in Linux.

### Network backup

All of the preceding backup strategies can be performed over a network. This is good because you can share a single backup device with many computers on a network. This is much cheaper and more convenient than installing a tape drive or other backup device in every system on your network. If you have many computers, however, your backup device will require a lot of capacity. In such a case, you might want to consider a mechanical tape loader, DVD-RW drive, or CD or DVD jukebox (which is capable of recording multiple CDs or DVDs without operator intervention).

It is even possible to do a form of disk mirroring over the network. For example, a Web server may store a duplicate copy of its data on another server. If the first server crashes, a simple TCP/IP hostname change can redirect the Web traffic to the second server. When the original server is rebuilt, it can recover all of its data from the backup server and be back in business.

## Selecting a Backup Medium

Armed with a backup strategy in mind, it's time to select a backup medium. Several types of backup hardware and media are available for use with Fedora and RHEL. Each type has its advantages and disadvantages.

The type of medium to choose depends largely on the amount of data you need to archive, how long you will store backups, how often you expect to recover data from your backups, and how much you can afford to spend. Table 13-1 compares the most common backup media.

The following sections describe how to use magnetic tape, writable DVDs, and writable CDs as backup media. Using additional hard drives as backup media is described later in this chapter.

## Table 13-1: Comparison of Common Backup Media

| Backup Medium | Advantages | Disadvantages |
| :---- | :---- | :---- |
| Magnetic tape | High capacity, low cost for archiving massive amounts of data. | Sequential access medium, so recovery of individual files can be slow. |
| Writable CDs | Random access medium, so recovery of individual files is easier. Backups can be restored from any CD-ROM drive. | Limited storage space (up to 700MB per CD). |
| Writable DVDs | Random access medium (such as CDs). Large capacity (4.7GB, although the actual capacity you can achieve might be less). DVD-R9 and DVD-9 DVDs can store up to 8.5GB of data. | DVD-RW drives and DVD-R disks are relatively expensive (although they are coming down in price). As more manufacturers add DVD writers to their PCs, DVD will eventually replace CDs as the most common removable media drives. |
| Additional hard drive | Allows faster and more frequent backups. Fast recovery from crashes. No media to load. Data can be located and recovered more quickly. You can configure the second disk to be a virtual clone of the first disk, so that you can boot off of the second disk if the first disk crashes. | Data cannot be stored offsite; thus there is a risk of data loss if the entire server is destroyed. This method is not well suited to keeping historical archives of the many revisions of your files. The hard drive will eventually fill up. By using removable hard drives, you can overcome this limitation by removing the backup drive when it is full and moving it to a secure location. |

## Magnetic tape

Magnetic tape was for years the most common medium used for backing up large amounts of computer data. Tapes provide a low-cost, convenient way to archive your files. Today’s high-capacity tape drives can back up many gigabytes of data on an amazingly small tape, allowing vast amounts of information to be safely stored. Tapes are also easy to transport offsite so that data will be secure in case of fires, hurricanes, or other disasters.

The primary disadvantage of magnetic tape is that it is a sequential access medium. This means that tapes are read or written from beginning to end, and searching for a particular file can be time-consuming. For this reason, tape is a good choice for backing up and restoring entire file systems, but not the ideal choice to recover individual files on a regular basis.

Fedora and RHEL can use a wide variety of tape drives. Most SCSI tape drives will work without loading special modules. Even many IDE tape drives are now supported natively, without requiring the drive to operate in a “SCSI emulation” mode. Some drives, however, require installation of additional software.

### Using ftape tools for magnetic tape

If your tape drive is attached to an IDE floppy controller cable, you will need to use the ftape driver to access it. Fortunately, the ftape loadable module is bundled with the Linux 2.6 kernel. When your Linux system boots, it should autodetect the tape drive and load the ftape driver. To verify that your system loaded the tape driver, type the following command shortly after you boot your computer:

```
dmesg | grep ftape
```

This searches the most recent kernel messages for lines containing the word ftape. If the ftape module was loaded, you should see something like this:

```
ftape v4.04d 25/11/97
[000] ftape-init.c (ftape_init) - installing OIC-117 floppy tape hardwire drive... .
[001] ftape-init.c (ftape_init) - ftape_init @ 0xd00b0060.
[002] ftape-buffer.c (add_one_buffer) - buffer nr #1 @ c1503914, dma area @ c02c0000.
[003] ftape-buffer.c (add_one_buffer) - buffer nr #2 @ c1503c44, dma area @ c0298000.
[004] ftape-buffer.c (add_one_buffer) - buffer nr #3 @ c50abaac, dma area @ c0328000.
[005] ftape-calibr.c (time_inb) - inb() duration: 1109 nsec.
[006] ftape-calibr.c (ftape_calibrate) - TC for 'ftape_udelay(1)' = 310 nsec (at 20479 counts).
[007] ftape-calibr.c (ftape_calibrate) - TC for 'fdc_wait(1)' = 2208 nsec (at 2559 counts).
```

If the module was not loaded, then you should check whether your kernel is compiled with support for the ftape module and your particular tape driver. It should be available and ready to include as a loadable module.

In most cases, an ftape device can be accessed just like a SCSI device. The primary difference is that an ftape device file contains the letters qft (for OIK Floppy Tape) where a SCSI tape contains st. For example, the device file for the first SCSI tape on your system will probably be /dev/st0; the device file for the first floppy tape will likely be /dev/qft0.

All of the standard tape- and archiving-related programs should work fine with both types of hardware. Nevertheless, there are a few extra programs that you might find useful when working with a floppy tape drive. These programs can be found in the mt-st package in Fedora. The mt command is used to control magnetic tape operation. The stinit command can initialize SCSI magnetic tape drives.

### Testing the magnetic tape drive

With the mt-st package installed, you should now be ready to test your tape drive. Insert a blank tape into the tape drive and type the following commands:
