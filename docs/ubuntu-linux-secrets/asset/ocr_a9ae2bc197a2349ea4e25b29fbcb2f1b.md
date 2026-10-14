Many advanced server systems use a small computer system interface (SCSI) hard drive controller instead of an IDE controller. SCSI controllers typically allow up to seven devices per controller channel (although some newer ones allow 16 devices). These controllers are popular in servers that support multiple hard drives in a redundant array of inexpensive disk (RAID) configuration. RAID systems use multiple hard drives to emulate a single hard drive for fault-tolerance purposes. There are several formats of RAID support:

+   - RAID0: Divides data among multiple hard drives but without redundancy.
+   - RAID1: Writes all data to two or more drives (called mirroring).
+   - RAID2: Incorporates error detection codes within stored data.
+   - RAID3: Stores data across several drives at the byte level, reserving one drive to store a parity bit. The parity bit is used to rebuild an individual drive if it fails.
+   - RAID4: Stores data across several drives at the block level, reserving one drive to store a parity bit.
+   - RAID5: Stores data across several drives at the block level; also writes a parity bit for each block on the drives.

RAID1 is common when only two hard drives are present. One hard drive is the primary, and the other is a hot backup. The disk controller performs all disk write requests from the operating system on both hard drives. RAID3 and RAID5 are the most popular methods of RAID disk support and usually require three or more hard drives. Both of these methods can recover data from a complete failure of any one disk in the system.

Despite the "inexpensive" part of its name, RAID technology can be expensive, and it is used primarily for high-availability server environments. The Ubuntu server installation can detect and use most SCSI controllers and RAID configurations.

However, don't confuse a hardware RAID environment with a software RAID. Many Windows servers allow you to emulate a RAID environment using standard disk hardware. This is called a software RAID because there aren't multiple disks, but the operating system acts as if there are. Ubuntu will work with standard disk drives, but it won't emulate a RAID environment using them.

# Partitioning an Existing Hard Drive

Partitioning an existing hard drive is the most complicated method for installing Ubuntu on an existing workstation. Normally, if you have an existing operating system on your workstation (such as Windows XP or Vista), it uses the entire hard drive installed on the PC. During installation, Ubuntu allows you to split the hard drive into multiple sections, called partitions. It will then install the operating system on the new partition. The original operating system still resides on the first partition, allowing you to run it, just as before, in a dual-boot configuration.

Before you run the Ubuntu installation, you'll want to know what your particular hard drive setup is, so you'll know how much space you can allocate for Ubuntu. Here are the steps in preparing your existing hard drive for the Ubuntu installation.