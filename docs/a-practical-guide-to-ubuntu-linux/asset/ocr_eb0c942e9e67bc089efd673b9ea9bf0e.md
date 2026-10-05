# PLANNING THE INSTALLATION

the kernel. You can preserve some user data during an installation depending on where it is located and how you format/partition the hard disk. Alternatively, you can perform a clean install on an existing system without overwriting data by setting up a dual-boot system (page 76).

# If you have a system running Ubuntu, upgrade install of

Ubuntu recommends that, if you have a system running Ubuntu and to run a newer release, you upgrade the release on the system. The rationale for this recommendation is twofold. First, the upgrade path is more aggressively tested by Ubuntu developers than the installers. You are less likely to run into problems with an update. Second, an upgrade preserves the system settings and applications, making an upgrade easier than a clean install.

Upgrade replaces all installed software packages with the most recent version available on the new release. During an upgrade, the installation program preserves both configuration and user data files. An upgrade brings utilities that are present in the old release up-to-date and installs new utilities. If you upgrade your system, back up all files on the.

In general, all new features are provided by an upgrade. However, GRUB is not automatically updated to GRUB 2 (page 584) during an upgrade. For information on upgrading from GRUB to GRUB 2, see help.ubuntu.com/community/Grub2. See page 74 for instructions on upgrading an Ubuntu to a new release. See www.ubuntu.com/getubuntu/releases to learn about features that will not take effect with an upgrade.

# SETTING UP THE HARD DISK

A hard disk must be prepared in several ways so Linux can read and write from it. Low-level formatting is the first step in preparing a disk for use. You do not need to perform this, as it is done at the factory where the hard disk is manufactured. The next steps in preparing a hard disk for use are to create a partition table and to create partitions on the disk. Finally, you need to create a filesystem on each partition. A partitioned disk that is not occupied by partitions is called free space. A new disk has no partition table, no partitions, and no free space. Under DOS/Windows, the term formatting creating a filesystem on a partition; see “Filesystems”

A partition, or a section of a hard disk that has a device name, as /dev/sda1, so you can refer to from other sections. For normal use, you must create at least one partition on a hard disk (pages 34 and following). From a live system, and after you install Ubuntu, use the Gnome Partition Utility (page 66) to view, resize, and create partitions on an existing system. During installation, use the graphical editor (page 60 and 70) or the textual partition editor (page 87) to create partitions. After installation, you can use parted (page 611) or fdisk to manipulate partitions. /dev on page 488 for more information on device names.

A partition table holds information about the partitions on a hard disk. The first partition can be created on a disk, the program creating it must set