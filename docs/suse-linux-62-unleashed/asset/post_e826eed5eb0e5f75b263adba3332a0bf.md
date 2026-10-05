
# SuSE System Administration
PART III

> Note
The only characters that are illegal in UNIX filenames are the slash and the ASCII NUL.

These backup utilities are written specifically to write backups to any kind of file; in fact, they were designed for sequentially accessed character devices, such as tape drives.

# Linux Filesystems

When you have more than one item of data, it is necessary to have some method of organizing files on the device. These methods are called filesystems. Linux enables you to choose any organizational method to marshal your files on its storage device. For example, you can use the MS-DOS filesystem on a floppy or the faster ext2 filesystem on your hard disk.

Many different filesystems are supported by Linux; the ext2 filesystem is used most because it is designed for Linux and is very efficient. Other filesystems are used for compatibility with other systems; for example, it's common to use the mdos and vfat filesystems on floppies; these are the native filesystems of MS-DOS and Windows 95. Under SuSE Linux 6.2, support for various filesystems may be available to the kernel by default (in this instance, the EIDE kernel as selected during the install):

```
$ cat /proc/filesystems
ext2
minix
msdos
vfat
nodev proc
iso960
nodev hpfs
nodev devpts
```

Support for other filesystems is available as loadable modules:

```
$ ls -R /lib/modules/
adfs
autofs
binfmt_aout
binfmt_elf
binfmt_java
binfmt_misc
coda
ext2
fat
hfs
hpfs
isofs
minix
msdos
ncpfs
nfs
nls_cp437
nls_cp737
nls_cp775
nls_cp850
nls_cp852
nls_cp855
nls_cp857
nls_cp860
nls_cp861
nls_cp862
nls_cp863
nls_cp864
nls_cp865
nls_cp866
nls_cp869
nls_cp874
nls_iso_859-1
nls_iso_859-2
nls_iso_859-3
nls_iso_859-4
nls_iso_859-5
nls_iso_859-6
nls_iso_859-7
nls_iso_859-8
nls_iso_859-9
ntfs
qnx
romfs
smbfs
sysv
ufs
vfat
```

Some of (nfs, ncpfs, and smbfs) are network filesystems that’t depend on block devices. Network filesystems are covered in Chapter 15, “NFS: Network File System.” Other filesystems are supported by Linux but are not provided by the standard kernel.

> Tip
Besides checking for loadable kernel modules, another good place to look for the types of supported filesystems is under the /usr/src/linux/ directory in the file.c. SuSE supports more than 20 types of filesystems.

# Managing Filesystems
CHAPTER 18

## The mount command

Use the mount command to mount a block device onto the filesystem. You need to specify what device contains the filesystem, what it is, and where in the directory hierarchy to mount it.

A mount command looks like

```
mount [-t type] [-o options] device mount-point
```

device must be a block device; if it contains a colon, it can be the name of another machine from which to mount a filesystem. mount-point should be an existing directory (or you will get an error); the filesystem will appear at this position. (Anything previously in that directory will be hidden.) The filesystem type and options are optional, and the variety and meaning of options depend on the type of filesystem being mounted. If the filesystem you want to mount is specified in the SuSE table, or /etc/fstab, you only need to specify the mount point or the device name:

```
# mount /cdrom
```

The necessary command-line options are derived from the /etc/fstab entry. However, to mount a filesystem at any point in your file system without using the default SuSE /etc/fstab entry, you must supply all the required options for the mount command:

```bash
# mount /dev/fd0 -t vfat /mnt/floppy
```

In this example, a floppy vfat filesystem is mounted at the mount point /mnt/floppy (which must first exist, the default SuSE mount point is /floppy). For example, some installation scripts, such as Sun Microsystems’ StarOffice 5.1a, require the source CD-ROM to be mounted at a specific point in the filesystem. To mount a CD-ROM at /mnt/cdrom directory, you must first create that directory, and manually mount the CD-ROM, supplying a filesystem type following the -t option, a proper device for the CD-ROM ( /dev/vdhd in this example), and finally, a mount point:

```bash
# mkdir /mnt/cdrom
# mount -t iso9660 /dev/vdhd /mnt/cdrom
```

Mounting a different filesystem, such as a vfat, or iso9660 CD-ROM causes the Linux kernel to automatically load the vfat or iso9660 driver into the kernel when needed. The kernel module handler loads these drivers, and when they become unused after the filesystem is unmounted, they are unloaded to recover the memory they occupied. See Chapter 23, “Kernel Management,” for more information about kernel modules.

# Potential Problems

Any of several things can cause the mount command to fail:

- Incorrect device name—It is possible to specify a device that does not exist or for which driver is not available.
- Unreadable devices—Devices can be unreadable either because the media are bad or because you have insufficient permissions to mount.
- Bad mount point—Trying to mount at a point that does not exist.
- An incorrect /etc/fstab entry—Incorrectly spaced, typed, entries may cause problems.
- Other errors—Still more error conditions are possible, for example, exceeding the number of loopback devices.
