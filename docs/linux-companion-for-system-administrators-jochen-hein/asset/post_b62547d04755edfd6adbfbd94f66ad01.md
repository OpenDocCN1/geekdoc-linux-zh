
# WHY EVERYBODY NEEDS BACKUPS 205

many files, you should use the possibility to run them 'out of the wood' by inserting an echo in front of the command proper (Listing 7.2).

```
(Linux):"find -name \*" -exec rm {}\;
(Linux):"find -name \*" -exec rm {}\;
(Linux):"find -name \*" -ok rm {}
```

# Listing 7.2 Dry execution of dangerous commands.

The first command displays the list of all files to be processed; in the second command, these files are actually deleted. Another possibility for using the output of the command is to redirect the output into a shell. The third command in Listing 7.2 ensures that for each file found the user is prompted to confirm that the command should actually be executed. A further alternative for the deletion of backup copies is shown in Listing 7.3.

```
(Linux):"find -name \*"
(Linux):"rm $(find -name \*)"
```

# Listing 7.3 Dry execution of dangerous commands, another way of doing it.

In case of a power failure or system crash, sometimes not all data is written to the hard disk. LINUX, unlike other UNIX systems and modern versions of the MS-DOS cache smartdrv, implements a write cache, in which write accesses are buffered before the data is written to the hard disk. This makes writing to the hard disk substantially faster for the action, and therefore has more time to carry out other functions.

After a system crash, the file system may be in a non-recoverable state, if some data is lost. In the worst case, even a total loss of data is possible, if the internal structure of the file system is no longer consistent. The Extended-2 file system, widely used under LINUX, has been implemented with a view to farreaching reparability, these problems occur relatively rarely. Most errors of this kind are caused by defective hardware. A number of new file systems are being developed that be more stable in case of a system crash, and faster to repair. File systems keep a log or journal of pending operations that only these need to be applied. Until now, ext3 and reiserfs have not been part of the kernel but are available as patches. Additionally IBM and SGI are porting their JFS (from OS/2) and XFS (from IRIX).

The first superblock of the file system, which contains the most important information on this file system, could be damaged. The program for checking Extended-2 file systems, e2fsck and fsck.ext2, can be instructed to use a backup copy of the superblock via the command line option -b. Listing 7.4

# 206 BACKUP

shows a possible way of proceeding. The first superblock is located in the first block, further superblocks can be found every 8192 blocks of the partition.

```
(Linux):# fsck.ext2 -f -v /dev/hdb1
efsck 0.5b, 14-Feb-95 for EXT2 FS 0.5a, 94/10/23
efsck: Bad magic number in super-block while trying to
open /dev/hdb1
```

The file system superblock is corrupt. Try running efsck with an alternate superblock using the -b option. (8193 is commonly an alternate superblock; Hence, 'efsck -b 8193 <device> may recover the file system.)
(Linux):# fsck.ext2 -f -v -b 8193 /dev/hdb1

Listing 7.4 Example of a corrupted superblock.

With the structure of the LINUX directory tree and the powerful utilities, it is relatively easy to save the user and configuration files. In the standard installation, the necessary tools are available, for example, if you store /home in a separate partition.

It is however, important that not the backup is executed on an error-free medium. The system administrator should also check the restoring of individual files and, if at all possible, the entire system. Only after such a check can you be sure that the data has been effectively backed up and can also be restored. This test should obviously be rerun if changes are made to the system software used (kernel, hardware drivers, libraries, backup system) or to the hardware.

In particular, it is sensible to create an emergency diskette which contains all drivers and programs needed to restore the system. Then, a minimal system can initially be booted from the floppy disk, so that no data from the hard disk is needed. This makes it possible to always restore a backup, even if the system on the hard disk is no use.

There are several freely available packages for the creation of emergency diskettes, ... If in doubt, the boot and root diskettes of the corresponding distribution are a good starting point; modern systems and distributions can also boot from CD, which makes things particularly easy. Some packages for the creation of emergency and boot diskettes can be found on the ftp server sunsite.unc.edu in the directory /pub/Linux/system/Recovery.

# SURVIVING DISK ERRORS WITH RAID 207

## 7.2 Surviving disk errors with RAID

From the point of view of the operating system, modern hard disks are error-free for a relatively long time. If, however, the first error is signalled, it is time to replace this disk. Usually, you will carry out a last backup and then restore the hard on to the new hard disk.

During the time in which the data is backed up and restored and the hard disk replaced, no system operation is possible. Thus, it is time, even in the case of disk damage, to run the system until the next period of reduced activity, to replace the disk in peace and quiet. Some modern SCSI adapters and disks are 'hot-plug' capable, that is, they can be replaced during normal operation, but this is not always possible.

With RAID (Redundant Array of Inexpensive Disks) technology, a procedure has been developed which is capable of surviving the failure of one or more disks without loss of data. Unfortunately, this technology does not prevent accidental erasure or inconsistencies after a system crash.

RAID technology has a series of levels which describe the kind of data storage in more detail. Currently, the following are the most widely used levels:

- RAID-0 is used to combine several disks or partitions into one larger (virtual) partition. There are two variations, the simple concatenation of the parts (concat) and striping. In striping, consecutive blocks are not put on one disk after the other, but are distributed in stripes across all disks involved. This achieves a higher performance, especially if the hard disks are connected to different SCSI adapters. Data security, however, decreases, so loss of data must be expected if one of the disks is defective.
- Data security is improved with RAID-1, which is mirroring. Here, each block is written in parallel to two or more disks, so that in case of failure of one hard disk, the data can still be accessed. When reading, the load can be distributed across several disks, and thus a higher data throughput can be achieved. The cost of this solution is relatively high because all hard disks must be doubled.
- In RAID-4, in addition to the data, a so-called parity is stored. If one disk fails, the data can still be reconstructed from the other disks. The disadvantage of this solution is that each write process must also take place on the parity disk. The advantage is that comparatively few additional hard disks are needed.
- Most frequently, RAID-5 is used which combines the advantage of RAID-4 with a parity distributed across all disks. Thus, data throughput does not decrease to the same extent as with RAID-4.

All of these solutions can be realized by means of special hardware (a SCSI adapter with a corresponding disk array) or software. The current versions of the LINUX kernel implement these functions.

Before you rejoice - RAID is not the solution to all problems. With RAID, you can protect yourself against the failure of one hard disk. If, however, the corresponding hard disk controller gives in, the most reliable mirror is good for nothing. In the same way, RAID does not protect you against system crashes or accidental erasure of data. Therefore, you should carry out periodical backups with RAID.

| ftp server: | ftp.kernel.org |
| --- | --- |
| ftp path: | /pub/linux/daemons/raid |
| File: | raidtools-0.41.tar.gz |
| Size: | about 40 Kbytes |
| Home page: | http://lin.as.org/linux/raid.html |

## 7.3 Backup media

With today’s hard disk sizes, a complete backup on diskettes have become practically impossible. The expense in time and backup media is out of all proportion to the security to be gained. Nevertheless, backups on diskets of small amounts of data which need backing up are possible and make sense. The text of this book was backed up on diskette after each change.

Frequently, magnetic tapes are used as backup media. Tapes are inexpensive and, despite the sequential access, sufficiently fast. There are several different standards for magnetic tapes and the corresponding drives or interfaces to which tri can be connected. The best known standards are the QIC (Quarter Inch Cartridge) standards.

### 7.3.1 Floppy streamers

On PC systems, floppy streamers that can be connected to the floppy disk controller are very popular. These devices can read and write magnetic tapes have QIC-40 or QIC-80 format. Recently, systems with higher capacity have appeared.
