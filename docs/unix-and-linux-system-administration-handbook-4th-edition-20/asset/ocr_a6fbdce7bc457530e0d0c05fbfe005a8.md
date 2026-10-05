# Chapter 8 Storage

Significantly, GPT retains primitive compatibility with MBR-based systems by dragging an MBR as the first block of the partition table. This “fakie” MBR makes the disk look like it’s occupied by one large MBR partition (at least, up to the 2TB limit of MBR). It isn’t useful per se, but the hope is that the decoy MBR may at least prevent naïve systems from attempting to reform the disk.

Versions of Windows from the Vista era forward support GPT disks for data, but only systems with EFI firmware can boot from them. Linux and its GRUB loader fared better: GPT disks are supported by the OS and bootable on any system. Intel-based Mac OS systems use EFI and GPT partitioning. Solaris understands GPT partitioning, and ZFS uses it by default. However, Solaris disks cannot use GPT partitioning.

Although GPT has already been well accepted by operating system kernels, its support among disk management utilities is still patchy; GPT remains a “bleeding edge” format. There is no compelling reason to use it on disks that don’t require it (that is, disks 2TB in size or smaller).

# Linux partitioning

Linux systems give you several options for partitioning, fdisk is a basic command-line partitioning tool. GNU’s parted is a fancier command-line tool that understands label formats (including Solaris’s native one) and can move and resize partitions in addition to simply creating and deleting them. A GUI version, gparted runs under GNOME. Another possibility is cfdisk, which is a nice, terminal-based alternative to fdisk.

parted and gparted can theoretically resize several types of filesystems along with the partitions that contain them, but the project home page describe this feature as “buggy and unreliable.” Filesystem-specific utilities are likely to do a better job of adjusting filesystems, but unfortunately, parted does not have a “resize the partition but not the filesystem” command. Go back to fdisk if this is what you need.

In general, we recommend gparted over parted. gparted lets you specify the size of the partitions you want instead of specifying the starting and ending block ranges. For partitioning the boot disk, most graphical installers are the best option since they typically suggest a partitioning plan that works well with that particular partition’s layout.

# Solaris partitioning

ZFS automatically labels disks for you, applying a GPT partition table. However, you can also partition disks manually with the format command. An fdisk command is also available. Both interfaces are menu driven and relatively straightforward. On x86 systems.

format gives you a nice list of disks to choose from, while fdisk requires you to specify the disk on the command line. Fortunately, format has an fdisk command