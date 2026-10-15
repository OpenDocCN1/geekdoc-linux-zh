# Client-Initiated Backups

As with server-initiated backups, you must reverse the steps you took to back up the data when you perform a client-initiated restore. This might involve the following:

+   - Restoring files from a tape backup and then copying them to the client system with a backup utility or ordinary file sharing.
+   - Mounting a removable disk and using client-side backup software or file sharing to recover files from the disk.

The details, of course, vary substantially from one implementation to another.

Tip
If you used the image-within-an-image procedure to back up a Macintosh by using Disk Copy, you can restore the image directly from your Linux share. There's no need to create a new disk image and place the backup image in the new disk image. Of course, if you've already got such an image, you can restore the backup file to the empty image if you like.

# CD-R Backups

If you use tar to create a backup on a CD-R disc, you should follow the same procedures you would for restoring from tape. If you created an ISO-9660, Joliet, or HFS CD-ROM by using mkisofs or mkhybrid, however, you can restore the files using only the client system—simply insert the CD-R into the client system's CD-ROM drive and read the files from the CD-R disc. You can do the same if you used Apple's Disk Copy utility and burned the resulting image file to CD-R. Of course, you can restore files by mounting the CD-R on the Linux computer and sharing it, but unless the client system doesn't have a CD-ROM drive, sharing the mounted CD-R is the more complicated solution.

# Complete Restores and Disaster Recovery

Partial restores are fairly easy, but if the client system doesn't boot, you have a much more difficult task ahead of you. This is particularly true of Windows systems because floppy boots don't give you full access to Windows long filenames or (for Windows NT and 2000) NT File System (NTFS)

No matter what approach you take to disaster recovery, you should attempt to test your solution before disaster strikes. You can do this either by using your chosen solution to restore a limited number of files or by attempting to restore an entire installation to a spare hard disk or empty disk partition. Doing a complete restore has the advantage that you can check to be sure the system will boot.