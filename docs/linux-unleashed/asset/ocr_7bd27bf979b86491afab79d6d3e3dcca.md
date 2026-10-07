# Linux and Hard Disk Layouts

To understand how LILO works, it is necessary to understand how a hard disk is laid out. You probably already know that a hard disk is essentially a set of concentric tracks, radiating out from the center of the disk platter. Each track is divided into a number of sectors.

Hard disks are identified by the number of platters (or, more accurately, the number of heads: The number of platters can be greater than the number of heads because one or more surfaces—typically the top and bottom—might not be used for data storage), the number of tracks per inch of disk platter (measured radially), and the number of sectors per track. The capacity of each sector leads to the total capacity of the disk by multiplying the number of sectors per track, the number of tracks, and the number of platters with heads.

Linux is usually integrally tied with DOS, so it is useful to look at the way DOS uses a hard disk. A single-purpose (single DOS operating system, for example) hard disk (and most floppy disks) have a boot sector followed by a data area that includes an administrative block.

The boot sector is the first sector on the hard disk and is read when the system starts to load the operating system. The boot sector essentially contains a bootstrap to direct the machine to the startup routines.

The administrative block is usually part of the data area, although it is commonly not accessible directly by users. The administrative area contains the administrative tables that show file locations in terms of *head/track/sector*. DOS uses the File Allocation Table (FAT), while UNIX and Linux use the superblock or i-node tables. The administrative table is not usually read until the boot process has been started.

The data area is used to store files (including the operating system startup code). Each file on the hard disk will have an entry in the administrative block that indicates the file-name and physical location on the hard disk. Other information is usually also stored in the administrative block (such as owner, permissions, date and time, and so on, depending on the operating system).

When there is lots of space on a hard disk, you will probably want to install more than one partition (probably supporting more than one operating system, such as providing both DOS and Linux on the same disk). You can create up to four “primary” partitions on a DOS disk.

![](bbox=[0.84, 0.6, 1.0, 0.77])