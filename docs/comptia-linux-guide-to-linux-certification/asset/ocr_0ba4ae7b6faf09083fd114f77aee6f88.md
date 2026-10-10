+   Many different filesystems are available to Linux; each filesystem is specialized for a certain purpose, and several different filesystems can be mounted to different mount points on the directory tree. You can create a filesystem on a device using the `mkfs` command and its variants.

+   The LVM can be used to create logical volumes from the free space within multiple partitions on the various hard disks within your system. Like standard hard disk partitions, logical volumes can contain a filesystem and be mounted to the Linux directory tree. They allow for the easy expansion and reconfiguration of storage.

+   USB and Firewire storage devices are recognized as SCSI disks by the Linux system.

+   It is important to monitor disk usage using the `df`, `du`, and `du --max-depth=2` commands to avoid running out of storage space. Similarly, it is important to check disks for errors using the `fsck` command and its variants.

+   If hard disk space is limited, you can use hard disk quotas to limit the space that each user has on filesystems.

# Key Terms

/dev directory  The directory off the root where device files are typically stored.

/etc/fstab  A file used to specify which filesystems to mount automatically at boot time and queried by the mount command if an insufficient number of arguments are specified.

/etc/mtab  A file that stores a list of currently mounted filesystems.

/proc/devices  A file that contains currently used device information.

bad blocks  The areas of a storage medium unable to store data properly.

block  The unit of data commonly used by filesystem commands; a block can contain several sectors.

block devices  The storage devices that transfer data to and from the system in chunks of many data bits by caching the information in RAM; they are represented by block device files.

btfsfs command  A command used to configure btfs filesystem options and check btfs filesystems for errors.

cfdisk command  A command used to partition hard disks; displays a graphical interface in which the user can select partitioning options.

character devices  The storage devices that transfer data to and from the system one data bit at a time; they are represented by character device files.

cylinder  A series of tracks on a hard disk that are written to simultaneously by the magnetic heads in a hard disk drive.

device file  A file used by Linux commands that represents a specific device on the system; these files do not have a data section and use major and minor numbers to reference the proper driver and specific device on the system, respectively.

df (disk free space) command  A command that displays disk free space by filesystem.

du (directory usage) command  A command that displays directory usage.