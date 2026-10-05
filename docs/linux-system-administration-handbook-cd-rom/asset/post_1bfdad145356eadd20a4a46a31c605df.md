
# Chapter 20 • Backing Up Your Data

- Multiple backup devices—when one is full, it will move to the next device in the list.
- Locking files during backup to allow safer backups in multiuser mode.
- Support for all file types, including sockets, pipes, and so forth.

More information on PerfectBACKUP + is available from http://home.xl.ca/perfectBackup/.

## BACKUP/9000

Though this is available only in beta for Linux as of this writing, it has one feature that prompted us to include it. It is designed to work with Oracle to allow live, safe backups of Oracle's tablespaces. If you are running Oracle (for SCO using the IBSC emulation, there is no native Linux version), you will undoubtedly find this feature of great use. Beyond this, Backup/9000 supports what you would expect of a commercial backup and restore program:

- Nice user interface.
- Scheduling tool.
- Support for local and network backups
- Uses tar or cpio format
- Encryption
- Parallel backups to multiple local and/or network tape backups
- Backup of raw partitions and FIFO streams in addition to normal files
- Multiple backups on one tape

## 20.5 Backup Strategies

How often you make what kind of backup depends on several factors, including:

- The capacity and speed of your backup device, particularly important for unattended backup.
- How active your file systems are. What percentage of files are changing per day or week? Most likely, this will vary from partition to partition.
- Whether or not you can make live backups.

## 20.6 RAID and Disk Mirroring

- If you can't make live backups, how much downtime is acceptable and when is it least inconvenient.

In general, more than a few percent of a particular filesystem is changing daily, you should perform incremental backups every day or two, a lower-level backup weekly, and a full backup monthly. Lower activity levels mean you can space this out, though there's really no excuse for not performing a full backup once a month.

Buy lots of whatever your backup media is; it's cheaper than having to pay the office for a day of working a second time.

For very active systems which more or less cannot be taken off-line except at 3 A.M. on a Sunday, you should get a commercial backup utility that will perform safe, live backups at least during low traffic periods. You will then hopefully be able to perform unattended incremental backups at night, fully backups if you can fit the system on one tape.

The more databases are typically problematic when it comes to live backups. Usually, your backup utility cannot make a proper snapshot from the database's point of view. Fortunately most databases can create a snapshot of themselves, and that can be placed in your archive. Failing this, the database will have to be taken off-line before being backed up.

You will probably want to keep some backups off-site in case of a disaster (flood, UFO crashing into your system, dinosaur rampage, etc.). You may have to buy a new system, but at least you'll have what is likely hundreds, if not thousands, man-hours of work saved.

These are other techniques for protecting the integrity of your data. RAID stands for Redundant Array of Inexpensive Disks. It is a fairly new concept, having been introduced in 1987 at the University of California, Berkeley.

The basic idea behind RAID is that by using small disks (as opposed to few large disks) and possibly some additional "parity" data, you will be able to reconstruct data loss when one of the disks fails instead of losing a few gigabytes (albeit temporarily, assuming that you have a backup).

There are several levels of RAID, clearly numbered from 0 to 5. Their features are given in the following table. Only levels 1, 4, and 5 are available for Linux, and only in software (as opposed to a hardware level implementation).

| Level | Description |
| :--- | :--- |
| 0 | Data striping—This doesn't actually provide any protection against data loss but does enhance performance. Requires a controller that supports synchronized disks; none are available for Linux. |
| 1 | Disk mirroring—A second set of disks are used to provide a complete copy of data. An expensive option, since you need twice as many disks. |
| 2 | Level 0 with a check disk for storing error correction information. Poor performance has made this option unpopular. |
| 3 | Level 0 with a separate disk for byte-level parity information to reconstruct lost data. If the parity disk is lost, you lose all data integrity. Synchronized disks help boost performance despite the bottleneck of the single parity disk. |
| 4 | Level 3 with block level parity information stored on a separate disk. Better performance but worse performance than level 3. Since synchronized disks aren't used, it can be implemented in software. |
| 5 | Level 4 with the parity information spread over the disks as well. Higher performance since a separate parity disk is no longer a potential bottleneck. Write performance is still not as good as level 3. |

To implement RAID on your Linux box, you need a kernel patch available from http://www.linuxhq.com/patch/20-p0632.html and a 2.0.30 kernel. The patch is still in beta and supports RAID levels 1, 4, and 5.

Separately available, raidtools-0.3 can be used to create or repair a set of RAID disks.

## 20.7 Summary

A variety of backup data and restore tools were discussed, ranging from simple ones that ship with every Linux distribution to commercial ones with enhanced functionality and interfaces.

In general, for sites where short amounts of down time is acceptable, the built-in tools are fine. For 'hot' backups, you will probably have to resort to commercial means.

# Chapter 21 Talking to Your Peripherals

It’s not all disk drives and video cards!

As anyone knows, there are many more resources to be shared, served, and managed than applications and disk volumes (though we will cover adding disks, too). Scanners, modems, printers, tape drives, and Zip and Jaz drives can all be made available to other machines on your LAN.

Printer setup and sharing are covered in a separate chapter, because other than disk sharing, the printer is the most frequently shared resource.

One problem that frequently plagues PCs with many peripherals is IRQs or interrupt conflicts. There are a number of ways to deal with these which will be discussed at the end of this chapter.

## 21.1 Scanners

Most scanners can be purchased in either SCSI or parallel port form. Currently Linux supports only scanners connected via a SCSI adapter. The canonical way to talk to a scanner via Linux is an adaptation of the xv program known as xvscan. Xscan is a commercial program that is available for $50 from tummy Ltd. (http://www.tummy.com/xvscan/).

Typically SCSI scanners will come with their own, low-grade SCSI card. Unless you are running out of SCSI IDs, it is not going to be worth your while to attempt use Linux to talk to the scanner through this controller, assuming a Linux driver exists for it.

Your kernel will need to have the generic SCSI driver compiled in it or as a module. You will need to check and possibly set the SCSI ID of your device. The device responding to the scanner will then be /dev/scsi[a-f]. Here "a" would be a SCSI ID of 0; "b" would be 1; and so on up to "f" which would have an ID of 6.

xvscan communicates with the scanner via /dev/scanjet, so you will have to create a link to the device or a copy of it. Also, you will need to modify the permissions of the device to be able to access the scanner.

Assuming your scanner's SCSI ID is 3, its device entry is

```
crw-rw-rw- 1 root sys 21, 3 Aug 28 00:12 /dev/sgd
```

To set up a copy of the device to users in the scanner group, issue the following commands as root:

```
# mkmod /dev/scanjet 21 33
# chgrp scanner /dev/scanjet
# chmod 660 /dev/scanjet
# ls -1 /dev/scanjet
crw-rw-rw---- 1 root scanner 21, 3 Aug 28 00:15 /dev/scanjet
```

## 21.2 Modems

There are a number of reasons you might want to attach a modem to your machine:

- Faxing—incoming and outgoing
- Backup (or primary!) network connection
- Dial-up for remote access

If you have an external modem, the only issue you have to worry about having the serial port driver available. If you have an internal modem, which adds its own serial port to your machine, you may run into IRQ problems.
