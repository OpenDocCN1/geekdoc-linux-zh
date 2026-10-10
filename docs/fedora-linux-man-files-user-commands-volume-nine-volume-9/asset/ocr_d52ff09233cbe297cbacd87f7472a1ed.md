# **Other operating systems**

This version of **syslinux** supports chain loading of other operating systems (such as MS-DOS and its derivatives, including Windows 95/98).

Chain loading requires the boot sector of the foreign operating system to be stored in a file in the root directory of the filesystem. Because neither Linux kernels, nor boot sector images have reliable magic nuers, **syslinux** will look at the file extension. The following extensions are recognised:

+   none or other Linux kernel image BSS Boot sector (DOS superblock will be patched in) BS Boot sector

For filenas given on the command line, **syslinux** will search for the file by adding extensions in the order listed above if the plain filena is not found. Filenas in KERNEL statements st be fully qualified.

# **Novice protection**

**Syslinux** will attempt to detect if the user is trying to boot on a 286 or lower class machine, or a machine with less than 608K of low (“DOS”) RAM (which ans the Linux boot sequence cannot complete). If so, a ssage is displayed and the boot sequence aborted. Holding down the Ctrl key while booting disables this feature.

The compile ti and date of a specific **syslinux** version can be obtained by the DOS command “type ldlinux.sys”. This is also used as the signature for the LDLINUX.SYS file, which st match the boot sector

Any file that **syslinux** uses can be marked hidden, system or readonly if so is convenient; **syslinux** ignores all file attributes. The SYSUNIX installed automatically sets the readonly attribute on LDLINUX.SYS.

# **Bootable CD-ROMs**

SYSUNIX can be used to create bootdisk images for El Torito-compatible bootable CD-ROMS. However, it appears that many BIOSeare very buggy when it cos to booting CD- ROMS. So users have reported that the following steps are helpful in making a CD-ROM that is bootable on the largest possible nuer of machines:

+   Use the -s (safe, slow and stupid) option to SYSUNIX
+   Put the boot image as close to the beginning of the ISO 9660 filesystem as possible.

A CD-ROM is so ch faster than a floppy that the -s option shouldn’t matter from a speed perspective.

Of course, you probably want to use ISOLINUX instead. See the documentation file **isolinux.doc**.

# **Booting from a FAT partition on a hard disk**