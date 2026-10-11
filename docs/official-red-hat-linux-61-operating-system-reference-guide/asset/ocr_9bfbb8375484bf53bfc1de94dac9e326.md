> WARNING
> 
> If you choose Skip, you will not be able to boot your Red Hat Linux system directly, and will need to use another boot method (such as a boot disk). Use this option only if you are sure you have another way of booting your Red Hat Linux system!

# 10.11.1 Alternatives to LILO

If you do not wish to use LILO to boot your Red Hat Linux system, there are a few alternatives:

# Boot Disk

You can use the boot disk created by the installation program (if you elected to create one).

# LOADLIN

LOADLIN can load Linux from MS-DOS; unfortunately, it requires a copy of the Linux kernel (and an initial RAM disk, if you have a SCSI adapter) to be available on an MS-DOS partition. The only way to accomplish this is to boot your Red Hat Linux system using some other method (e.g., from LILO on a diskette) and then copy the kernel to an MS-DOS partition. LOADLIN is available from ftp://metalab.unc.edu/pub/Linux/system/boot/dualboot/ and associated mirror sites.

# SYSLINUX

SYSLINUX is an MS-DOS program very similar to LOADLIN; it is also available from ftp://metalab.unc.edu/pub/Linux/system/boot/loaders/ and associated mirror sites.

# Commercial Bootloaders