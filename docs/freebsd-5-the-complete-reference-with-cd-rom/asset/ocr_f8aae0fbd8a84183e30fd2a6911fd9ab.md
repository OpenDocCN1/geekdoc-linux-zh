In the future, other interfaces are likely to play an increasingly important role. In particular, IEEE-1394 (aka FireWire) may become the successor to SCSI for at least some purposes. IEEE-1394 hard disks are already available. Support for FireWire in FreeBSD 5.0 is very limited.

To learn which EIDE controllers and SCSI host adapters are supported, consult the *HARDWARE.TXT* file that comes with FreeBSD. Note that this file focuses on *chips*; the specific brand and model device in your computer may not be listed, even if it's supported. Check the names of the chips on a PCI card to learn what you have. If Windows is currently installed on your system, you can use the Windows System control panel to learn something about it: Click the Device Manager tab and expand the Hard Disk Controllers item. For instance, Figure 1-2 shows a computer that uses a VIA EIDE controller (*IDE* is an older standard that evolved into EIDE, and some utilities continue to use the older term, as in Figure 1-2).

> **Note**
> 
> *You don't need drivers for specific EIDE or SCSI devices. For instance, if you change your EIDE CD-ROM drive for another EIDE CD-ROM drive, you don't need to update your FreeBSD CD-ROM drivers because these device use standardized command sets. You do need drivers for most specific EIDE or SCSI device types, such as hard disk or CD-ROM drivers. These drivers are included in the standard FreeBSD kernel, so their use is usually transparent.*

![](bbox=[0.15, 0.55, 0.85, 0.93])

**Figure 1-2.** *Windows can be a useful tool for discovering what hardware a computer has.*