# ISO 9660 CD-ROM Filesystem Support

Most CD-ROMs use this filesystem. The filesystems on CDs meant for Unix systems typically use the Rock Ridge extension, also included in the driver.

# Minix fs Support

Best built as a module, the Minix filesystem is small and best suits slow devices such as floppy disks. If you need to compile it directly into the kernel, you’re probably using a Minix RAM disk image.

# /proc Filesystem Support

Modern Linux tools use the /proc filesystem for system status, kernel parameters, and other miscellaneous configuration. Compile it directly into your kernel.

# Network File Systems

You’ll find NFS, Coda, and SMB stuff here; all are client-side components and don’t include server code. There’s a way to look at SMB shares without kernel support using SAMBA (see Section 4.2 for information).

# 7.3 Building the Kernel

Now that you’ve got your kernel configured, it’s time to compile it.

# Verify Source Files

First run the following commands:

```
```text
# make clean
# make dep
```
```

These commands attempt to verify that you have all of the required source files in place on your system. They take a little while to run; output should appear as in the following fragment:

```
```text
make[1]: Entering directory `/usr/src/linux-2.2.12/arch/i386/boot'
make[1]: Nothing to be done for `dep'.
make[1]: Leaving directory `/usr/src/linux-2.2.12/arch/i386/boot'
scripts/mkdep init/*.c > .depend
scripts/mkdep `find /usr/src/linux-2.2.12/include/asm /usr/src/linux-2.2.12/include/linux /usr/src/linux-2.2.12/include/scsi /usr/src/linux-2.2.12/include/net -follow -name \*.h | -name modversions.h -print` > hdepend
...
```
```