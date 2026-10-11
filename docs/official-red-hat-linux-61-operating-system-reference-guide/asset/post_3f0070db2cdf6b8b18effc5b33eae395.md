
## B.1.7 Disk Partitions and Mount Points

One area that many people new to Linux find confusing is the matter of how partitions are used and accessed by the Linux operating system. In DOS/Windows, it is relatively simple: If you have more than one partition, each partition gets a "drive letter." You then use the drive letter to refer to files and directories on a given partition.

This is entirely different from how Red Hat Linux deals with partitions and, for that matter, with disk storage in general. The main difference is that each partition is used to form part of the storage necessary to support a single set of files and directories. This is done by associating a partition with a directory through a process known as **mounting**. Mounting a partition makes its storage available starting at the specified directory (known as a **mount point**).

For example, if partition `/dev/hda5` were mounted on `/usr`, that would mean that all files and directories under `/usr` would physically reside on `/dev/hda5`. So the file `/usr/doc/FAQ/txt/Linux-FAQ` would be stored on `/dev/hda5`, while the file `/etc/X11/gdm/Sessions/Gnome` would not.

Continuing our example, it is also possible that one or more directories below `/usr` would be mount points for other partitions. For instance, a partition (say, `/dev/hda7`) could be mounted on `/usr/local`, meaning that, for example, `/usr/local/man/whatis` would then reside on `/dev/hda7` rather than `/dev/hda5`.

## B.1.8 How Many Partitions?

At this point in the process of preparing to install Red Hat Linux, you will need to give some consideration to the number and size of the partitions to be used by your new operating system. The question of "how many partitions" continues to spark debate within the Linux community and, without any end to the debate in sight, it's safe to say that there are probably as many partition layouts as there are people debating the issue.

Keeping this in mind, we recommend that, unless you have a reason for doing otherwise, you should create the following partitions:

- A swap partition -- Swap partitions are used to support virtual memory. In other words, data is written to swap when there is not RAM to hold the data your system is processing. If your computer has 16 MB of RAM or less, you *must* create a swap partition. Even if you have more memory, a swap partition is still recommended. The minimum size of your swap partition should be equal to your computer’s RAM, or 16 MB (whichever is larger).

### Intel

The following partition is specific to Red Hat Linux/Intel installations.

- A `/boot` partition -- The partition mounted on `/boot` contains the operating system kernel (which allows your system to boot Red Hat Linux), along with a few other files used during the bootstrap process. Due to the limitations of most PC BIOSes, creating a small partition to hold these files is a good idea. This partition should be no larger than 16MB.

**Please Note**

> Make sure you read Section B.1.9, *One Last Wrinkle: Using LILO* -- the information there applies to the `/boot` partition!

![image](img/eda1471ab4ce718c791c97a85559a478_317_0.png)

The following partition is specific to Red Hat Linux/Alpha installations.

- A MILO partition -- Alpha owners that will be using MILO to boot their systems should create a 2MB DOS partition where MILO can be copied after the installation is complete. We recommend using /dos as the mount point.

- A root partition ( / ) -- The root partition is where / (the root directory) resides. In this partitioning layout, all files (except those stored in /boot) reside on the root partition. Because of this, it's in your best interest to maximize the size of your root partition. A 600MB root partition will permit the equivalent of a workstation-class installation (with very little free space), while a 1.5GB root partition will let you install every package.

## B.1.9 One Last Wrinkle: Using LILO

LILO (the Linux LOader) is the most commonly used method to boot Red Hat Linux on Intel-based systems. An operating system loader, LILO operates "outside" of any operating system, using only the Basic I/O System (or BIOS) built into the computer hardware itself. This section describes LILO's interactions with PC BIOSes, and is specific to Intel-compatible computers.

### BIOS-Related Limitations Impacting LILO

LILO is subject to some limitations imposed by the BIOS in most Intel-based computers. Specifically, most BIOSes can't access more than two hard drives and they can't access any data stored beyond cylinder 1023 of any drive. Note that some recent BIOSes do not have these limitations, but this is by no means universal.

All the data LILO needs to access at boot time (including the Linux kernel) are located in the /boot directory. If you follow the partition layout recommended above, or if you are performing a workstation- or server-class install, the /boot directory will be in a small, separate partition. Otherwise, it will reside in the root partition. In either case, the partition in which `/boot` resides must conform to the following guidelines if you are going to use LILO to boot your Red Hat Linux system:

### On First Two IDE Drives

If you have 2 IDE (or EIDE) drives, `/boot` must be located on one of them. Note that this two-drive limit also includes any IDE CD-ROM drives on your primary IDE controller. So, if you have one IDE hard drive, and one IDE CD-ROM on your primary controller, `/boot` must be located on the first hard drive only, even if you have other hard drives on your secondary IDE controller.

### On First IDE or First SCSI Drive

If you have one IDE (or EIDE) drive and one or more SCSI drives, `/boot` must be located either on the IDE drive or the SCSI drive at ID 0. No other SCSI IDs will work.

### On First Two SCSI Drives

If you have only SCSI hard drives, `/boot` must be located on a drive at ID 0 or ID 1. No other SCSI IDs will work.

### Partition Completely Below Cylinder 1023

No matter which of the above configurations apply, the partition that holds `/boot` must be located entirely below cylinder 1023. If the partition holding `/boot` straddles cylinder 1023, you may face a situation where LILO will work initially (because all the necessary information is below cylinder 1023), but will fail if a new kernel is to be loaded, and that kernel resides above cylinder 1023.

As mentioned earlier, it is possible that some of the newer BIOSes may permit LILO to work with configurations that don't meet our guidelines. Likewise, some of LILO's more esoteric features may be used to get a Linux system started, even if the configuration doesn't meet our guidelines. However, due to the number of variables involved, Red Hat cannot support such extraordinary efforts.

**Please Note**

Disk Druid as well as the workstation- and server-class installs take these BIOS-related limitations into account.

## C Driver Disks

## C.1 Why Do I Need a Driver Disk?

While the Red Hat Linux installation program is loading, you may see a screen that asks you for a driver disk. The driver disk screen is most often seen in three scenarios:

- if you are running the installation program in expert mode
- if you run the installation program by entering linux dd at the boot: prompt
- if you run the installation program on a computer which does not have any PCI devices

### C.1.1 So What Is a Driver Disk Anyway?

A driver disk adds support for hardware that is not otherwise supported by the installation program. The driver disk could be produced by Red Hat, it could be a disk you make yourself, or it could be a disk that a hardware vendor includes with a piece of hardware.

There is really no need to use a driver disk unless you need a particular device in order to install Red Hat Linux. You will most likely use a driver disk for SCSI adapters and NICs, as those are really the only devices which are used during the installation that might require driver disk support. If an unsupported device is not needed to install Red Hat Linux on your system, continue with a regular installation and then add support for the new piece of hardware once the installation is complete.

### C.1.2 How Do I Obtain a Driver Disk?

Your best option for finding driver disk information is on Red Hat’s website at http://www.redhat.com/support/errata/ under the section called **Bug Fixes**.

If you find a driver disk that is appropriate for your device support needs, create a boot disk using that filename.img file. For instructions on how to make a boot disk, see the *Official Red Hat Linux Installation Guide* section called *Making Installation Diskettes*.
