backups of particular OSs or hosts. For example, you might back up Linux one week and Windows the next, with incremental backups of each on alternating days.

Try to design your desired backup schedule before setting on a tape drive. This way, you'll be able to narrow your search to drives that are well suited to this schedule. You can rule out drives with insufficient capacity or speed, for example. If you plan to do nightly backups of a home computer in a room adjacent to your bedroom, you might want to favor quiet drives, so as to reduce the likelihood that you'll be disturbed by the sound of the backup. (Some Travan drives sound disturbingly like a dentist's drill.)

# Tape Backup Interfaces

As with other data storage devices, the type of interface used on a tape drive is of critical importance to the drive's operation, and to how it interacts with other devices on your system. It should come as no surprise that SCSI and EIDE/ATAPI are the two major interfaces used on tape drives today, although a few other interfaces are also available.

# SCSI Interfaces

As with many other devices, the SCSI interface is the interface of choice for tape backup drives. There are several reasons for this, including

+   • SCSI allows both internal and external devices, so it's possible to use one external SCSI tape backup device to back up several computers, even without using network backup tools.
+   • A SCSI bus can support up to 7 or 15 devices, depending upon the SCSI variant, as compared to only 2 devices for EIDE. This advantage is reduced, however, when mixing Ultra2 or faster SCSI devices with lesser SCSI variants, because Ultra2 or faster devices work best on SCSI buses that don't have slower varieties.
+   • The SCSI bus supports fully multitasking operation, which can reduce the likelihood of shoe-shining. If you put an ATAPI tape drive on the same chain as an EIDE hard disk, the computer must stop sending data to the tape drive in order to read data from the hard disk. This can cause the tape drive's buffer to run dry, necessitating a reversal in tape direction. This scenario is less likely when using SCSI devices because SCSI supports simultaneous access to two or more drives.
+   • As a general rule, the variety of tape drives is greater for SCSI than for EIDE or other interfaces. In particular, the highest-performance drives are available only in SCSI form. Even at the low end, SCSI drives aren't rare, except for drives of such low capacity that they're obsolete.