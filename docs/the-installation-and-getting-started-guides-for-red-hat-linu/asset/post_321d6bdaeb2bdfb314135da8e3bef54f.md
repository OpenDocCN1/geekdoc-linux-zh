
debating the issue. Keeping this in mind, we recommend that, unless you have a reason for doing otherwise, you should create the following partitions:

- **A swap partition** — Swap partitions are used to support virtual memory. If your computer has 16 MB of RAM or less, you must create a swap partition. Even if you have more memory, a swap partition is still recommended. The minimum size of your swap partition should be equal to your computer's RAM, or 16 MB (whichever is larger). The largest useable swap partition is roughly 127 MB, so making a swap partition larger than that will result in wasted space. Note, however, that you can create and use more than one swap partition if your system requires more than 127MB of swap. The following partition is specific to Red Hat Linux/Intel installations.

- **A /boot partition** — The partition mounted on /boot contains the operating system kernel, along with a few other files used during the bootstrap process. Due to the limitations of most PC BIOSes, creating a small partition to hold these files is a good idea. This partition should be no larger than 16MB. Please Note: Make sure you read Disk Partitions and Other Operating Systems — the information there applies to the /boot partition!

- **A root partition** — The root partition is where / (the root directory) resides. In this partitioning layout, all files (except those stored in /boot) reside on the root partition. Because of this, it's in your best interest to maximize the size of your root partition. A 500MB root partition will permit the equivalent of a workstation-class installation (with very little free space), while a 1GB root partition will let you install every package.

## One Last Wrinkle: Using LILO

LILO (the Linux LOader) is the most commonly used method to boot Red Hat Linux on Intel-based systems. An operating system loader, LILO operates "outside" of any operating system, using only the Basic I/O System (or BIOS) built into the computer hardware itself. This section describes LILO's interactions with PC BIOSes, and is specific to Intel-compatible computers.

## BIOS-Related Limitations Impacting LILO

LILO is subject to some limitations imposed by the BIOS in most Intel-based computers. Specifically, most BIOSes can't access more than two hard drives and they can't access any data stored beyond cylinder 1023 of any drive. Note that some recent BIOSes do not have these limitations, but this is by no means universal. All the data LILO needs to access at boot time (including the Linux kernel) are located in the /boot directory. If you follow the partition layout recommended above, or you are performing a workstation- or server-class install, the boot directory will be in a small, separate partition. Otherwise, it will reside in the root partition. In either case, the partition in which /boot resides must conform to the following guidelines if you are going to use LILO to boot your Red Hat Linux system:

On First Two IDE Drives — If you have 2 IDE (or EIDE) drives, /boot must be located on one of them. Note that this two-drive limit also includes any IDE CD-ROM drives on your primary IDE controller. So, if you have one IDE hard drive, and one IDE CD-ROM on your primary controller, /boot must be located on the first hard drive only, even if you have other hard drives on your secondary IDE controller.

On First IDE or First SCSI Drive — If you have one IDE (or EIDE) drive and one or more SCSI drives, /boot must be located either on the IDE drive or the SCSI drive at ID 0. No other SCSI IDs will work.

On First Two SCSI Drives — If you have only SCSI hard drives, /boot must be located on a drive at ID 0 or ID 1. No other SCSI IDs will work.

Partition Completely Below Cylinder 1023 — No matter which of the above configurations apply, the partition that holds /boot must be located entirely below cylinder 1023. If the partition holding /boot straddles cylinder 1023, you may face a situation where LILO will work initially (because all the necessary information is below cylinder 1023), but will fail if a new kernel is to be loaded, and that kernel resides above cylinder 1023.

As mentioned earlier, it is possible that some of the newer BIOSes may permit LILO to work with configurations that don't meet our guidelines. Likewise, some of LILO's more esoteric features may be used to get a Linux system started, even if the configuration doesn't meet our guidelines. However, due to the number of variables involved, Red Hat Software cannot support such extraordinary efforts. Please Note: Disk Druid as well as the workstation- and server-class installs take
