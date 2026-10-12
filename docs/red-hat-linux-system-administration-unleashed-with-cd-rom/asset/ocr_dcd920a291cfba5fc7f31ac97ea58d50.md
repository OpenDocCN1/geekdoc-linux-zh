Now that you have an idea of what you need to back up and where to back it up to, all you need to decide is how often to do backups, and how long to keep the backed-up files. This is what is meant by a backup strategy.

# Backup Strategies

If you think about, you can come up with a plan that will make life much easier. As a system administrator, you are required by law to be lazy (the First Computer Law is “THINK!”—it is an effort to cancel out Murphy’s Law). A good system administrator will think for two days to save three keystrokes—or at least that’s my excuse!

Deciding on a backup strategy is actually quite easy, once you know what you need.

In the real world, there is no one correct way to implement backups, and thus no ideal backup strategy that works for everybody. The closest you can get to an ideal situation is to back up every file constantly, so that the difference between the original and the backup is a matter of seconds, or perhaps minutes. High-availability systems will need to implement this particular strategy at any cost. This usually is implemented by using hardware RAID 5 (Redundant Array of Independent Disks at level 5). To quote from the Software-RAID Mini-Howto (this document is available on your Red Hat Linux filesystem under `/usr/doc/HOWTO/mini`, if you installed the documentation):

> > Q: What is RAID?
> > A: RAID stands for “Redundant Array of Inexpensive Disks”, and is meant to be a way of creating a fast and reliable disk-drive subsystem out of individual disks. In the PC world, “I” has come to stand for “Independent”, where marketing forces continue to differentiate IDE and SCSI. In its original meaning, “I” meant “Inexpensive as compared to refrigerator-sized mainframe 3380 DASD”, monster drives which made nice houses look cheap, and diamond rings look like trinkets.

Hardware RAID consists of a special hard drive controller and several hard drives. The data is placed on the hard drives independently of the operating system, using one of a number of scenarios that the system administrator has chosen. These are known as RAID levels. There are several RAID levels, each with its own advantages and disadvantages.

RAID-0 is striping—just using several hard drives as though they were one larger one.

RAID-1 is mirroring—two hard drives each have the exact same data on them.

Higher levels of RAID incorporate things such as parity drives and combinations of the lower-level features (striping, mirroring, parity, and so on). Software RAID works, but is not as fast or reliable as hardware-based RAID.