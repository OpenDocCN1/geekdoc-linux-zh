|Table 2-1 Example minimum partition sizes^a (continued)
|/usr|Minimum of 2-16 gigabytes; depends on which and how many software packages you install
|/var|Minimum of 500 megabytes-much larger if you are running a server

a. The sizes in this table assume you create all partitions separately. For example, if you create a 1-gigabyte / (root) partition and do not create a /usr partition, in most cases you will not have enough room to store all the system programs.|

# RAID

RAID (Redundant Array of Inexpensive/Independent Disks) employs two or more hard disk drives or partitions in combination to improve fault tolerance and/or performance. Applications and utilities see these multiple drives/partitions as a single logical device. RAID, which can be implemented in hardware or software (Fedora/RHEL gives you this option), spreads data across multiple disks. Depending on which level you choose, RAID can provide data redundancy to protect data in the case of hardware failure.

True hardware RAID requires hardware designed to implement RAID and is not covered in this book (but see "Fake RAID" below).

Do not replace backups with RAID

Do not use RAID as a replacement for regular backups. If the system experiences a catastrophic failure, RAID is useless. Earthquake, fire, theft, and other disasters may leave the entire system inaccessible (if the hard disks are destroyed or missing). RAID also does not take care of the simple case of replacing a file when a user deletes it by accident. In these situations, a backup on a removable medium (which has been removed) or a network backup is the only way you will be able to restore a filesystem.

RAID can be an effective addition to a backup. Fedora/RHEL offers RAID software you can install either when you install a Fedora/RHEL system or as an afterthought. The Linux kernel automatically detects RAID arrays (sets of partitions) at boot time if the partition ID is set to 0xfd (raid autodetect).

Software RAID, as implemented in the kernel, is much cheaper than hardware RAID. Not only does this approach avoid the need for specialized RAID disk controllers, but it also works with the less expensive ATA disks as well as SCSI disks.

Fake RAID
Fedora/RHEL provides support for motherboard-based RAID (known as fake RAID) through the dmraid driver set. Linux software RAID is almost always better than fake RAID.

The partitioner on a live CD and an install DVD gives you the choice of implementing RAID level 0, 1, 5, 6, or 10: