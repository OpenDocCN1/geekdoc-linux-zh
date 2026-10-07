# # Supported SCSI Devices

You can’t assume that because Linux supports SCSI, any SCSI device will work. Most versions of the operating system have a hardware compatibility file in the distribution set that lists all devices that have been tested and known to work properly with the SCSI system. Check this file carefully before you buy a new device or controller card! Some devices and cards simply don’t work with Linux.

Some SCSI devices are shipped with their own kernel patches. You will have to make sure the patches correspond to the version of the Linux kernel you are using, then rebuild the kernel with the new drivers in place. If the devices don’t have a Linux kernel patch, check with the manufacturer or Linux distribution sites.

# # SCSI Device Drivers

Every device on the Linux system must have a device file, and SCSI devices are no different. In many cases, Linux is distributed with a complete set of SCSI device files that need only to be configured properly. You should know a little about device drivers, device files, and major and minor device numbers. See Chapter 33, “Devices,” for more information.

# ## Hard Drives

SCSI disk drives are always block devices and should always use major device number 8. No “raw” SCSI devices are usually supported by Linux despite its similarity to BSD UNIX, which does support raw SCSI devices.

Sixteen minor device numbers are allocated to each SCSI disk device. Minor device number 0 represents the whole disk drive, minor numbers 1 through 4 are the four primary partitions, and minor numbers 5 through 15 are used for any extended partitions.

With Linux, SCSI disk minor device numbers are assigned dynamically, starting with the lowest SCSI ID numbers. The standard naming convention for SCSI hard drives is `/dev/sd{letter}` for the entire disk device (such as `/dev/sda` or `/dev/sdb`), and `/dev/sd{letter}{partition}` for the partitions on that device (such as `/dev/sda1` or `/dev/sda2`).

Linux presents a few problems when partitioning SCSI disks, because Linux talks directly to the SCSI interface. Each disk drive is viewed as the SCSI host sees it, with block numbers from 0 up to the highest block number. They are all assumed to be error-free. This means there is an easy way to get at the disk geometry. (For comparison, DOS