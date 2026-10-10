# **Caution**

*No matter what backup medium you use, be alert to the security requirements of the media. Files that are inaccessible to normal users become readily accessible to anybody if your backup media can be easily “borrowed,” because common backup tools don’t enforce FreeBSD ownership and permissions restrictions. If a system contains sensitive data, you should be sure to store backups in a safe.*

# # Backup Media

The most common form of backup medium is magnetic tape. Tape drives cost between a hundred and several thousand dollars, depending upon their capacity, speed, and reliability. Tape drives you might use for a FreeBSD workstation or small server typically cost between $200 and $1500. The less expensive units in this range are *travan* tapes, which use expensive (roughly $40) tapes, and the more expensive units are *Digital Audio Tape* (*DAT*) units or various other medium devices, which typically use less expensive ($5 to $20) tapes. In the end, therefore, the cost of the units plus tapes varies by less than it first appears.

Tapes have the advantages of high capacity (modern units store tens of *gigabytes* per tape), reasonably high speed, and moderate cost per gigabyte backed up. Potential rival media types, such as removable disks, tend to be lower in capacity or much higher in cost. For instance, you’d need dozens of 100MB *Zip* disks to back up a modern computer, but you might be able to do the job with just one or two tapes.

One media type deserves special mention: optical discs. *Compact Disc Recordable* (CD-R) media store 650MB on a standard disc, which is enough (particularly when data are compressed) to hold a basic FreeBSD installation. If your installation is not too large, you may be able to back up a newly-installed system to CD-R for emergency recovery, and rely upon tapes for restoring user data. CD-R media are inexpensive, and they have the advantage of being readable on any computer, so in a networked environment, you can use them to restore clients even if those clients lack tape drives. CD-R media are also very reliable and have long expected shelf lives (between 20 and 100 years, by most estimates), so they make good archival media. Newer recordable *Digital Versatile Disc* (DVD) drives can record several gigabytes, and so can be even better backup devices, but in 2002 these drives are still more expensive than CD-Rs, and even read-only DVD drives still aren’t universal.

# # A Sample of Backup Tools

FreeBSD supports several backup programs. Most of these are designed for use with tapes, but they can be used with other backup media, as well. The more popular backup tools include


+   ■ **tar** The *tar* program is an old standard in the UNIX and FreeBSD world. Its name stands for *tape archiver*, and that’s what it does—create archives of data on tape. It’s also become a popular way to package files for distribution on the Internet and for storage on nontape removable media devices; *tar* can create