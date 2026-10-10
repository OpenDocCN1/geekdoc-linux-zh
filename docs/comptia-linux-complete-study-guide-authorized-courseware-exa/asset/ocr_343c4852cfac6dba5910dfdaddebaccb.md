was extended in a way that retained backward compatibility. The new scheme uses three partition types:

+   - *Primary partitions*, which are the same as the original partition types
+   - *Extended partitions*, which are a special type of primary partition that serves as a placeholder for the next type
+   - *Logical partitions*, which reside within an extended partition

Figure 3.3 illustrates how these partition types relate. Because logical partitions reside within a single extended partition, all logical partitions must be contiguous.

# FIGURE 3.3 The MBR partitioning system uses up to four primary partitions, one of which can be a placeholder extended partition that contains logical partitions.

![](bbox=[0.23, 0.34, 0.75, 0.4])

For any one disk, you’re limited to four primary partitions, or three primary partitions and one extended partition. Many OSs, such as DOS, Windows, and FreeBSD, *must* boot from primary partitions, and because of this, most hard disks include at least one primary partition. Linux, however, is not so limited, so you could boot Linux from a disk that contains no primary partitions, although in practice few people do this.

The primary partitions have numbers in the range of 1–4, whereas logical partitions are numbered 5 and up. Gaps can appear in the numbering of MBR primary partitions; however, such gaps cannot exist in the numbering of logical partitions. That is, you can have a disk with partitions numbered 1, 3, 5, 6, and 7 but not 1, 3, 5, and 7—if partition 7 exists, there must be a 5 and a 6.

In addition to holding the partition table, the MBR data structure also holds the primary boot loader—the first disk-loaded code that the CPU executes when the computer boots. Thus, the MBR is extremely important and sensitive. Because the MBR exists only in the first sector of the disk, it’s vulnerable to damage; accidental erasure will make your disk unusable unless you have a backup.

![](bbox=[0.13, 0.74, 0.21, 0.84])

> You can back up your MBR partitions by typing `sfdisk -d /dev/sda > sda-backup.txt` (or similar commands to specify another disk device or backup file). You can then copy the backup file (`/sda-backup.txt` in this example) to a removable disk or another computer for safekeeping. You can restore the backup by typing `sfdisk -f /dev/sda < sda-backup.txt`. Be sure you’re using the correct backup file, though; a mistake can generate incorrect or even impossible partition definitions!