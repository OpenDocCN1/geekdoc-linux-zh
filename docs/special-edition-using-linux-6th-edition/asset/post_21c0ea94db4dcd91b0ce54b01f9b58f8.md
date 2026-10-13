
## `/auto`

This directory is used to configure devices to automatically detect and mount removable media when loaded. For example, the CD-ROM drive can be configured to be automatically mounted after a CD-ROM is detected in the drive. This differs slightly from configuring the `/etc/fstab` file. The `/etc/fstab` file is used to predefine and, with the proper option, automatically mount a given device—at boot time—but it does not detect changes when a removable medium has changed.

## `/bin`

The `/bin` directory contains system and user utilities. This directory contains utilities that are mostly compiled code and are referred to as *binaries*, hence the directory name, `bin`. Some utilities in `/bin` are actually shell scripts. You can determine which are which by using the `file` command.

## `/boot`

This directory contains crucial components for the boot process, including a grub subdirectory. If you make changes that affect bootup, like adding a new kernel you want to boot from, you may have to make changes to your boot loaders. See Chapter 12, “Boot Loaders,” for more details on the boot loaders and the use of files contained in this directory.

## `/bru`

The `/bru` directory contains the components of a commercial add-on program for tape backups and restores. This directory is not defined as a part of the Filesystem Hierarchy Standard, but it meets the criteria of what is required for backup and restore capability. You will only have the `/bru` directory if you purchased BRU commercially. Other commercial programs will create their own directories, but normally do so below `/opt` or `/usr/local`.

## `/dev`

The `/dev` directory is where all the device definitions reside. The drivers themselves are in the `/lib/modules/[kernel version]/` directory, but the definition of a specific device is in this directory. Devices are discussed in detail at the end of this chapter. A number of subdirectories exist under `/dev` for device groupings.

Additionally, the 2.4.x kernel series introduced the devfs virtual filesystem. Distributions might opt not to use this new filesystem in the first distribution or two under the new kernel, but it will certainly figure in over time. The devfs filesystem functions similarly to the `/proc` filesystem (covered elsewhere in this chapter) in that it doesn’t exist until the system boots.

The reason for the development of such a system is that with the advent of IR and USB, the number of devices requiring a device file is exploding. With each static device file taking some hard disk space, the root filesystem would soon need to be extremely large to hold all the possible devices.

![](img/c741b1b6b6eccaba2ad43454c979a7f8_222_0.png)

With devfs, as a device is plugged in, a driver is loaded and devfs creates an entry for it in `/dev` dynamically and virtually. You will be able to work with it just as any real device node; it will just exist only in memory and not permanently on the disk.

The devfs filesystem uses devfsd to create devices on-the-fly. Your system will not show any devices in `/dev` that do not exist, so you will have gone from some 1200 or so entries to just a few hundred. Additionally, devfsd uses `/etc/devfsd.conf` to configure what types of devices show up. You can have the old `/dev/hda` devices (for example) or only the newer device names (the old names will be symlinks to the new ones).

> **Caution**
>
> Be careful making changes to `/etc/devfsd.conf`. This file must remain in sync with the names found in your `/etc/fstab` or you risk having an unbootable system until one or the other is fixed.

## `/etc`

The `/etc` directory might have been more aptly named the config directory because it contains configuration files and subordinate directories of system configuration data. It is important to be familiar with and understand the files in this directory. These files are crucial in the day-to-day operation and maintenance of your system. Whether it is a simple task, such as adding a user, or a more complicated task, such as configuring domain name resolution service, configuration files in `/etc` must be modified.

## `/home`

This is the directory that is used for user data. For example, each new user has a directory in the home directory when his or her account is activated. Upon logging in, a user is located in his or her home directory. If someone named Natalie were a newly added user, her home directory might be aptly named `/home/natalie`.

## `/initrd`

This directory is used in association with the requirement of an initial RAM disk for some system configurations. For example, initial ramdisk (initrd) support is often used to circumvent a chicken-and-egg scenario created when the driver for a SCSI hard disk is on the SCSI hard disk which can’t be mounted to access the driver until the driver is loaded. Loadable modules are discussed in detail in the chapter on system initialization.

## `/install`

This is a symbolic link to the directory in which install scripts and files are located, `/var/lib/LS`.

## `/lib`

Common libraries are stored in this directory. Different applications can make use of the same shared library. For example, the C programming code library itself is stored in this directory. With a name like `libc-2.1.3.so`, this library contains functions common to all C programs on the system. This enables programs to be smaller because they all refer to common functions in this library. Smaller programs save disk space, save RAM, and improve speed. This C library is essential; without it, the entire system (except the kernel) would stop running.

## `/lost+found`

Filesystem utilities to correct system errors store data (lost inodes) in this directory when attempts to fix the errors are unsuccessful or when files become truncated. You should find a `lost+found` directory at the top level of each mounted ext2 partition.

## `/mnt`

This directory is used for the default mount points for other filesystems. For example, by default the CD-ROM device mounts to `/mnt/cdrom`. The floppy disk drive mounts to `/mnt/floppy`. You are not required to use this directory for mount points, but it is provided for your convenience. If you are using the automount daemon, you can see filesystems mounted to `/auto`. But this is just for the automounter’s use. You should not use `/auto` for your mounts or you will confuse the automounter.

You are free to create and use (or just mount over) any directory you want, but beware of the possible consequences: If you mount over an existing filesystem, that filesystem becomes inaccessible.

## `/opt`

The `/opt` (options) directory is the directory in which add-on applications are installed. For example, the Netscape Communicator and Navigator packages are installed in the `/opt` directory. To comply with the Filesystem Hierarchy Standard, all third-party applications install to this directory.

## `/proc`

The `/proc` directory is actually a special filesystem. It contains detailed information about processes that are currently running, as well as specific information about hardware configurations. It’s commonly referred to as a process information pseudo-filesystem. It acts as an interface to kernel data structures. For example, the `/proc/interrupts` file contains information about which interrupts are being used. This is covered in more detail in the section, “Examining Key Directories.”

## `/root`

This directory is the home directory of the root user. By default, the root user logs in to this directory. Only files specific to the root user are stored in this directory. As noted earlier, this directory is not to be confused with the `/` directory, which is commonly referred to as the root directory.

![](img/c741b1b6b6eccaba2ad43454c979a7f8_224_0.png)

## `/sbin`

The `/sbin` directory contains system and administration utilities or binaries. Utilities for partitioning a hard drive, checking the integrity of a filesystem, creating a new filesystem, and shutting down or rebooting the system are all stored in this directory.

## `/tmp`

Temporary files are stored in this directory. Often, applications need to use temporary files with certain functions or when installing. These temporary files are stored in the `/tmp` directory.

## `/usr`

The `/usr` directory is intended for shareable, read-only data. It is the major section of the filesystem, but it can be configured to reside on a secondary machine. The majority of documentation is located in the `/usr/doc` directory. The complete source tree for the Linux kernel is located in the `/usr/src` directory.

## `/var`

The `/var` directory is set up to hold variable data. It contains spool directories for mail, news, print jobs, and other files, as well as other administrative files. All data logged by specific processes are stored in the `/var` directory.

## `/dev/shm`

Before moving on, one filesystem that mounts to the `/dev` directory by default (but can be mounted anywhere, including in the root directory) is the shm directory. This directory should never be used for anything. The kernel makes use of this filesystem for shared memory access. You can occasionally see a file or two written here that later disappear. The amount of shared memory available is calculated by the kernel at bootup, when the shared memory filesystem is mounted. It will be a portion of the entire virtual filesystem available to the kernel. Its size can be varied through `/proc/sys/kernel/shmmax`, but if you are not familiar with this filesystem, it is best to leave the value as-is.

> **Caution**
>
> If you are splitting your filesystem across multiple disks or partitions, the following directories must be in the root filesystem:
>
> - `/bin`, `/dev` (unless using the new devfs in lieu of `/dev`), `/etc`, `/lib`, `/root`
> - `/tmp`, `/var` (but some subdirectories of `/var`, such as the spool/mail subdirectory, are often NFS mounted from a central mailhost)
> - Also, some filesystems cannot be NFS-mounted (unless you are using a totally disk-less client)

You can determine what is mounted on your filesystem in one of several ways. The first way is to use `df`. This command shows you how much disk space is free for use on each mounted filesystem; however, not all filesystems will be shown.
