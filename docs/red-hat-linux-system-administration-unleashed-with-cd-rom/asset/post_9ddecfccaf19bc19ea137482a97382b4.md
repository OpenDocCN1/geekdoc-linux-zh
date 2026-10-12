
```
pd: pd version 1.0, major 45, cluster 64, nice 0
pda: Sharing parport1 at 0x378
pda: ep at 1.0, Shuttle EPAT chip c3 at 0x378, mode 5 (EPP-32), delay 1
pda: SyQuest EZ135A, 262144 blocks [128M], (512/16/32), removable media
pda: pda1
```

In order to access this device, you must create the appropriate device special files in the /dev directory. These devices should already exist on your Red Hat system; however, if they do not, there is a script in the file /usr/src/linux/Documentation/paride.txt that will create them for you. Once these devices are created, they are accessed just like other ATAPI/IDE devices, with the exception of the device name. Now that we have taken a look at the various types of removable media devices available for Linux, let's move on to the topic of granting access to users.

## Granting Access to Users

There are methods for allowing access to the removable media devices on your system without giving away root access. This section covers two of these options, one specifically for DOS filesystems, and the other a method for giving users the ability to mount removable media without compromising the security of the system. It also looks at using the automounter to mount removable media and some of the advantages and disadvantages of doing so. Please note that you probably do not want to give access to removable media devices to users on your server systems. The methods described here are most appropriate to workstations.

## The mtools Package

One method available for granting access to removable devices under Linux is via the mtools package. This package contains a number of commands that correspond to DOS commands and that are used to access DOS filesystem types, such as FAT and VFAT. Table 10.4 shows a list of some of the most common mtool commands, their DOS counterparts (if one exists), and what they do.

Table 10.4 mtools Commands

| Mtool Command | DOS Command | Description |
|---|---|---|
| mattrib | attrib | Sets the DOS file attributes on a file. |
| mbadblocks |  | Scans a disk for bad blocks and marks them. |
| mcd | cd | Changes directory on a DOS filesystem. |

### TABLE 10.4 continued

| Mtool Command | DOS Command | Description |
|---|---|---|
| mcopy | copy | Copies files to or from a DOS filesystem. |
| mdel | del | Deletes files from a DOS filesystem. |
| mdeltree | deltree | Deletes a directory and all files under it. |
| mdi | rdir | Displays a directory listing. |
| mdu |  | Shows the disk space usage of a DOS filesystem. |
| mformat | format | Does a minimal DOS format of the specified device. |
| mlabel | label | Sets the volume label on a DOS filesystem. |
| mmd | md | Creates a directory on a DOS filesystem. |
| mmove | move | Moves or renames a file or directory on a DOS filesystem. |
| mrd | rd | Removes a directory from a DOS filesystem. |
| mren | ren | Renames a file on a DOS filesystem. |
| mtype | type | Displays a text file on a DOS filesystem. |
| mzip |  | Issues Zip disk specific commands. Allows you to eject, write protect, remove write protection, and so on. |

The ability of these commands to access various devices that may contain DOS filesystems is determined by the /etc/mtools.conf file. On a default Red Hat installation, this file looks like this:

/etc/mtools.conf

```
# Example mtools.conf files. Uncomment the lines which correspond to
# your architecture and comment out the "SAMPLE FILE" line below

# Linux floppy drives
drive a: file="/dev/fd0" exclusive 1.44m
drive b: file="/dev/fd1" exclusive 1.44m

# First SCSI hard disk partition
#drive c: file="/dev/sda1"

# First IDE hard disk partition
#drive c: file="/dev/hda1"

# # dosemu floppy image
# drive m: file="/var/lib/dosemu/diskimage"

# dosemu hdimage
drive n: file="/var/lib/dosemu/hdimage" offset=8832

# Atari ramdisk image
# drive o: file="/tmp/atari_rd" offset=136

# ZIP disk for Solaris:
# Drive X is ZIP-100 at target 5
# drive X: file="/dev/rdsk/c0t5d0s2" partition=4 scsi=1 nodelay

# ZIP disk for SunOS:
# Zip drive is at target 5, which default kernel calls tape st1 !!
# drive Y: file="/dev/rdsk/c0t5d0s2" partition=4 scsi=1 nodelay

# autoselect zip drive/floppy on HP-UX 9/10
# drive a: file="/dev/rdsk/c0t0d5s0" exclusive partition=4
# drive a: file="/dev/rdsk/c0t0d5s0" exclusive partition=4
# drive a: file="/dev/rfloppy/c0t0d5s0" exclusive

#
# A/UX target 5 on 1st scsi bus jaz or zip
# drive X: file="/dev/rdsk/c0t5d0s31" partition=4

# Some examples for BeOS.
# floppy drive. hardcoded in devices.c, so no real need to define it here
#drive a: file="/dev/floppy_disk" exclusive
# ZIP drive on SCSI ID 6
#drive z: file="/dev/scsi_disk_060" offset=16384 fat_bits=16

# SCO Unix 3.2v4
# # Floppy disk drives
#
# drive a: file="/dev/install" exclusive
# drive b: file="/dev/install1" exclusive
#
# SCSI hard disk partitions
#
# drive c: file="/dev/dsk/0sC"
# drive d: file="/dev/dsk/0sD"
# drive e: file="/dev/dsk/0sE"
# drive f: file="/dev/dsk/0sF"
# drive g: file="/dev/dsk/0sG"
# drive h: file="/dev/dsk/0sH"

# # uncomment the following line to display all file names in lower
# # case by default
# mtools_lower_case=1
```

The comments in the file describe the purpose of each entry, and the manual page for mtools gives a more detailed description of how entries may be added to this file. In addition, the most detailed documentation of the mtools suite can be accessed on your Red Hat system by issuing the command

`info mtools`

or by looking up mtools using the info mode of Emacs.

The obvious drawback to the mtools suite is that it only works with DOS filesystems. Other than this, the mtools suite may be a simple solution to the problem of giving users access to removable devices. If their primary purpose is enabling “sneakernet” transfers of files, this may be enough.

## Giving Users the Power to Mount

Another option available to systems administrators is to grant users the ability to mount removable devices like floppy and CD-ROM drives through a special option to the mount command. Modern mount versions all support this option and enabling it consists of two steps. The first is to create mount points for the removable media devices and the second is to modify `/etc/fstab` to set the appropriate mount options to allow users access. Giving users the ability to mount removable media like floppies or CD-ROM drives is not a decision to be made lightly. It can be useful, however, so that users may transfer files between systems that are not networked.

## Creating Mount Points

Creating mount points may sound like a trivial exercise, but here are a few suggestions that may be helpful:

- Use a descriptive name for the mount points, such as /mnt/dosa for what would be the A drive in Windows or DOS.
- Create multiple mount points for different filesystem types so that users do not have to learn mount options.

By way of example, consider the following. User workstations all have a single floppy drive and an IDE CD-ROM drive accessible as /dev/cdrom. You want to allow users to mount floppies formatted for Linux (extended 2 filesystem) or DOS/Windows and data CDs. In this case, the mount points I would create would be:

- /mnt/dosA for DOS/Windows formatted floppies
- /mnt/fd0 for Linux formatted floppies
- /mnt/cdrom for data CDs

If I were to later add a Zip drive to a system and wanted to allow the user to mount either DOS or Linux formatted disks on it, I would add additional mount points:

- /mnt/zip for Linux formatted Zip disks
- /mnt/zipdos for DOS/Windows formatted disks

## Modifying /etc/fstab

To support user mounting of these types of drives, you must modify the filesystem table /etc/fstab. Here is a sample line from this file that demonstrates the two options you must specify in order to allow ordinary users to mount filesystems:

### /etc/fstab Entry

```
/dev/fd0  /mnt/fd0  ext2  noauto,nosuid,user,rw  1  0
```

In this entry, we specify a number of options. The first of these is the noauto option, which indicates that this filesystem should not be mounted automatically (that is, with the mount -a option). This is important mostly at boot time, when you will most likely not have a floppy in the disk drive and you do not want to wait for the floppy device to timeout. The next option is the nosuid option, which is an important security consideration and disallows the execution of setuid and setgid programs from the floppy. The user option is the key to allowing users to mount this filesystem. This option, which may only be set in the /etc/fstab file, tells the mount program to disable the check that the current user is root. This means that normal users are now permitted to mount the floppy device on the mount point /mnt/fd0 simply by issuing the command

```
mount /mnt/fd0
```
