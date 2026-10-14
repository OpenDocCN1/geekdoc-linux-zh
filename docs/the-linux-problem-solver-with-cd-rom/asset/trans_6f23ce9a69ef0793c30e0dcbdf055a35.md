
stuff that appears after you compile RAM disk support directly into the kernel (not as a module) has a new twist. Some distributions, such as Red Hat use this on SCSI-only systems to avoid compiling SCSI drivers into the kernel. They first boot with an initial RAM disk, then load a kernel module on that RAM disk (one containing the driver for the SCSI controller), then mount the true / partition. You can wiggle out of this mess by compiling the SCSI driver you need directly into the kernel, and changing /etc/lilo.conf before you run lilo (the part of LILO that installs the boot sector); Section 7.4 offers more on the subject.

## Networking Options

You can accept the default values here for most systems. Network firewalls and the options that appear after you choose it may be important if you're planning to do IP filtering or masquerading; turn to Section 2.4 for more details on that.

## SCSI Support

You usually know when you need SCSI support (you've got a SCSI host adapter), but the Linux kernel also considers external parallel port Zip drives to be SCSI devices.

## SCSI Disk Support

This turns on support for all sorts of hard disks, including removable-media disks.

## SCSI Generic Support

A number of miscellaneous devices use this driver, most commonly SCSI scanners and CD burners.

## SCSI Low-Level Drivers

Under this submenu, used to select drivers for individual SCSI controllers (host adapters), you may notice a few similar-looking entries if a device has more than one driver available (Symbios SCSI cards, for example), or if there is more than one version of the device (such as the two different versions of the parallel port Zip drive).

## Network Device Support

You'll find the network interface drivers, Ethernet, PPP, SLIP, token ring, and others here.

## Old CD-ROM Drivers

If you've got an older system with a proprietary CD-ROM drive, you might find support for it here. Most of these drives came with sound cards in some of the first multimedia kits, like the ones from Creative Labs or even MediaVision.

## Character Devices

You're best off leaving many of these options set, including Virtual terminal and Support for console on virtual terminal (not setting these will cause a system to break).

## Standard/Generic (Dumb) Serial Support

These are the standard PC serial ports that come with almost every computer. Modems, serial mice, UPS devices, and other gadgets hook up to serial ports (or emulate a serial interface).

## Parallel Printer Support

Enables I/O to printers on a parallel port. This only shows up if you select Parallel port support (and most likely will only be useful if you select PC-style hardware as well) under General setup.

## PROBLEM 80

> Symptom: Upon installation of a new kernel, the printer doesn't work anymore.
> 
> Problem: Renamed the printer device.
> 
> Fix: Starting with production release 2.2, printers begin at /dev/lp0 instead of /dev/lp1, so your former /dev/lp1 device file is now /dev/lp0. Usually the only place you have to change this is /etc/printcap.

## Mouse Support (not serial mice)

Selecting this enables a Mice submenu. Most modern mice use the so-called PS/2 port, for which the device is /dev/psaux. This submenu is not for mice that hook up to a serial port.

## Filesystems

It's fairly safe to compile most filesystems as modules, except for the second extended and /proc filesystems (see below); you will almost certainly need to compile these directly into the kernel (in fact, you're not even allowed to build /proc as a module).

## DOS FAT fs Support

Selecting this enables a few filesystems that use FAT, including the MS-DOS file system, UMSDOS (an extended MS-DOS filesystem), and the newer VFAT.

## ISO 9660 CD-ROM Filesystem Support

Most CD-ROMs use this filesystem. The filesystems on CDs meant for Unix systems typically use the Rock Ridge extension, also included in the driver.

## Minix fs Support

Best built as a module, the Minix filesystem is small and best suits slow devices such as floppy disks. If you need to compile it directly into the kernel, you’re probably using a Minix RAM disk image.

## /proc Filesystem Support

Modern Linux tools use the /proc filesystem for system status, kernel parameters, and other miscellaneous configuration. Compile it directly into your kernel.

## Network File Systems

You’ll find NFS, Coda, and SMB stuff here; all are client-side components and don’t include server code. There’s a way to look at SMB shares without kernel support using SAMBA (see Section 4.2 for information).

## 7.3 Building the Kernel

Now that you’ve got your kernel configured, it’s time to compile it.

## Verify Source Files

First run the following commands:

```
# make clean
# make dep
```

These commands attempt to verify that you have all of the required source files in place on your system. They take a little while to run; output should appear as in the following fragment:

```
make[1]: Entering directory `/usr/src/linux-2.2.12/arch/i386/boot'
make[1]: Nothing to be done for `dep'.
make[1]: Leaving directory `/usr/src/linux-2.2.12/arch/i386/boot'
scripts/mkdep init/*.c > .depend
scripts/mkdep `find /usr/src/linux-2.2.12/include/asm /usr/src/linux-2.2.12/include/linux /usr/src/linux-2.2.12/include/scsi /usr/src/linux-2.2.12/include/net -follow -name \*.h | -name modversions.h -print` > hdepend
...
```
