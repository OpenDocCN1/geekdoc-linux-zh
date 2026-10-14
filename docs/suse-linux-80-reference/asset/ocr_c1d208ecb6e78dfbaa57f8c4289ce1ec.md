Implementing LVM already makes sense for heavily used home PCs or small servers. If you have a growing data stock, as in the case of databases, MP3 archives, or user directories, the Logical Volume Manager is just the right thing for you. This would allow you file systems that are larger than physical hard disk. Another advantage of the LVM is up to 256 LVs can be added. Keep in mind that working with the LVM is very different than working with conventional partitions.

Instructions and further information on configuring the “Logical Volume Manager” (LVM) can be found in the official LVM HOWTO and the SuSE documentation:

+   - http://www.sistina.com/lvm/Pages/howto.html
+   - http://www.suse.com/us/support/oracle/.

# Soft RAID

The purpose of RAID (Redundant Array of Inexpensive Disks) is to combine several hard disk partitions into one large “virtual” hard disk for the optimization of performance and data security. Using this method, however, one advantage is sacrificed for another. “RAID level” defines the pool and common triggering device of all hard disks, known as the RAID controller. A RAID controller mostly uses the SCSI protocol, because it can drive more hard disks better than the IDE protocol. It is also better able to process parallel running commands. Instead of a RAID controller, which can often be quite expensive, the Soft RAID is also able to take on these tasks. SuSE Linux offers the option of combining several hard disks into one Soft RAID system with the help of YaST2 — a very reasonable alternative to Hardware RAID.

# Customary RAID Levels

**RAID 0** This level improves the performance of your data access. Actually, this is not really a RAID, because it does not provide data backup, but the name “RAID 0” for this type of system has become the norm. With RAID 0, two hard disks are pooled together. The performance is very good — although the RAID system will be destroyed and your data lost, even if just one of the many remaining hard disks fails.