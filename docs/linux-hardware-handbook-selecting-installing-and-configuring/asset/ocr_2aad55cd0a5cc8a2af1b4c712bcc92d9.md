# Using Recordable CDs for Backup

The low cost of CD-R and CD-RW media, and the high speed, random-access nature of these media, make them an appealing choice for backup media for many people. These drives weren’t intended as backup media, however, so there are several obstacles to be overcome—or at least, questions you must answer.

One problem is the limited capacity of the media. 650MB is not much space for backing up most Linux systems today. One solution is to plan your Linux installation so that no partition contains more than 650MB of data, or at least no more than is likely to fit in that space, given compression. You can then back up one partition at a time. Another solution is to use backup software that supports splitting your backup across multiple archives. Unfortunately, most such programs were designed for tapes and floppies, not CD-R discs, so integrating the backup software with the CD-R software can sometimes be a nuisance. Probably the best solution is to use DVD-RAM (or perhaps some other recordable DVD technology), which has higher capacity than CD-based drives.

Another challenge comes in the choice of backup software. The usual CD-recording formats can give you true random access to your data, but they alter filesystem characteristics. Most importantly, they remove waccess (which is meaningful on a read-only medium). Another option is to use tar or some similar archive program, and burn the resulting archive file onto the CD-R. You then lose some of the random-access characteristics of the medium, but you preserve your filesystem information just as if you’d used a tape drive.

My own preference is to use a tape backup drive for most backup functions. I do, however, use a CD-R drive to create backups of critical and seldom-changing configurations, particularly when I want the archive to be readable on a variety of computers. For instance, I back up Windows boot partitions using my CD-R drive under Linux.

Recordable drives do have their downsides, however, including

+   - **Speed** Although the read speed of CD-R drives is good enough for many purposes, it’s not as good as the best CD-ROM drives. Recording speed is invariably slower than is reading speed, so speeds are generally given as two numbers, such as 8×/24×, which is quite fast by the standards of early 2000. CD-R seek times are also higher than are those of CD-ROM drives, because the recordable heads are heavier and therefore take more time to safely move.

+   - **Expense** CD-R and CD-RW drives cost more than CD-ROM drives—usually between $200 and $400 in early 2000, although there are a few drives that cost more or less than this.

+   - **Delicacy** Recordable drives are more sensitive to damage than are CD-ROM drives, and are therefore more likely to break.