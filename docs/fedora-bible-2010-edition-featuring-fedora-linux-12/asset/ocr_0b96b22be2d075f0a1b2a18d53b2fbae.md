![](bbox=[0.18, 0.1, 0.63, 0.51])

Figure 12-1: Drag-and-drop files and folders on the CD/DVD Creator window for a simple backup. Click Burn on the Disk Burning Setup dialog to have the files and folders written to the disc.

# Doing a Simple Backup with rsync

Cheap hard disk space, fast networks, and some really neat new tools have given Linux users some nice backup alternatives to the old reliable removable media (such as tapes and CDs). To back up your personal data or the data from a small office computer, the examples in this section provide fairly simple ways of creating usable backups of your data.

To do this procedure, you need to have hard disk space on a computer that is at least slightly larger than the hard disk you are backing up. That hard disk space could be on:

+   - A different partition — By backing up to a separate disk partition on the same disk drive, you are protected in case the partition you are backing up becomes corrupted. However, you are not protected if your hard disk goes bad.

+   - A different hard disk — Backing up to a separate hard disk can protect from a corrupted disk, but won’t help you if your computer is hit by lightning, a flood, or other acts of God. It is also good to place the separate hard disk on a separate disk controller.

+   - A different computer — By backing up over the network, you can back up to another computer that is as far away from the source of your data as makes you feel comfortable. You can back up to the computer down the hall or one across the country.