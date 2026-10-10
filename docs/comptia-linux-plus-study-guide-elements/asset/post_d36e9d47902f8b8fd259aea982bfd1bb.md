
## Listing 1.1: Sample menu.lst File

```
default=0
timeout=4
splashimage=(hd0,3)/grub/splash.xpm.gz
title Linux (2.6.29)
    root (hd0,3)
    kernel /bzImage-2.6.29 ro root=/dev/hda9 mem=256M
    boot
title Windows
    rootnoverify (hd0,1)
    chainloader +1
    boot
```

> **NOTE** Chapter 3, “Managing Processes and Editing Files,” describes one of many text editors available for Linux.

Because GRUB wasn't designed exclusively for Linux, it introduces a new way of referring to hard disks and their partitions. Linux refers to hard disks using files in the `/dev` directory, such as `/dev/hda` and `/dev/hda9`. Disks may have names beginning with `hd` (for most PATA disks) or `sd` (for SCSI disks and most SATA disks). Following that string is a letter that refers to the physical disk, so a system could have, for instance, `/dev/sda` and `/dev/sdb`. Partitions on disks are given numbers starting with 1, as in `/dev/sda1` or `/dev/sdb7`.

GRUB uses strings of the form `(hdx,y)` to identify disks, where `x` is a disk number and `y` is a partition number. (The `y` and preceding comma may be omitted to refer to an entire disk or its MBR.) Both the `x` and the `y` are numbered starting from 0, which contrasts with Linux's numbering partitions starting with 1. Thus, Linux's `/dev/hda9` is GRUB's `(hd0, 8)`. GRUB doesn't distinguish between PATA and SCSI disks; `hd0` is the first disk recognized by the BIOS, `hd1` is the second disk, and so on.

The first three lines of Listing 1.1 set global options:

- **Default OS**: The `default=0` line tells GRUB to boot the first OS defined in the file by default. If this line read `default=1`, the default would be the second OS, and so on.
- **Timeout period**: The `timeout=4` line sets the timeout before booting the default OS to 4 seconds.
- **Splash image**: The third line in Listing 1.1 sets a splash image—an image that's displayed as part of the boot process. Many Linux distributions ship a splash image with their GRUB files to make for a fancier boot loader menu, but you can omit this line if you like. This example uses a GRUB-style hard disk specification to point to the image file. In this case, it's the `grub/splash.xpm.gz` file on the fourth partition on the first disk (probably `/dev/hda4` or `/dev/sda4`). Depending on where this partition is mounted, that could be `/grub/splash.xpm.gz`, `/boot/grub/splash.xpm.gz`, or some other location.

## Setting OS Boot Options

The two OS definitions in Listing 1.1 both begin with the keyword `title`, which provides a label for the OS that’s displayed by GRUB when it boots. Subsequent lines may be indented to help distinguish between the OS definitions, but this indentation is optional. Important features of OS definitions include the following:

**Root partition**: The `root` option identifies the GRUB root partition, which is the partition on which the GRUB configuration files reside. If you did *not* set aside a separate partition for `/boot` when you installed Linux, this line will identify the Linux root (`/`) partition, and subsequent file references will be relative to the Linux root partition. If you used a separate `/boot` partition, though, chances are the GRUB root partition will be the Linux `/boot` partition, and GRUB references to files in Linux’s `/boot` directory will omit that directory name. Listing 1.1 identifies the GRUB root partition as `(hd0, 3)`, which is `/dev/hda4` on a PATA system.

> **WARNING**
>
> GRUB can read files from several filesystems, including `ext2fs`, `ext3fs`, ReiserFS, FAT, and FFS. You can use any of these filesystems as your GRUB root partition. If you want to use another filesystem, such as JFS or XFS, as your Linux root partition, you should split off your GRUB root partition from the Linux root partition.

**Linux kernel**: The `kernel` option identifies a Linux kernel or a kernel for certain other Unix-like OSs, such as a GNU Hurd kernel. This reference is relative to the GRUB root partition, as defined by `root`. You can also pass kernel options on this line. Note that the `root` option passed to the Linux kernel identifies the Linux root partition using a Linux device filename, but the `root` option in the GRUB OS definition identifies the GRUB root partition. The two might be the same, but they might not be. In the case of Listing 1.1, they aren’t the same—the GRUB root partition is `(hd0, 3)`, or `/dev/hda4`, whereas the Linux root partition is `/dev/hda9`. Chances are `/dev/hda4` is the Linux `/boot` partition. The `ro` option passed on the `kernel` line tells the kernel to mount the root partition in read-only mode initially, just as the `ro` option does in `lilo.conf`.

**Root partition without verification**: The `rootnoverify` option works just like the `root` option, except that it tells GRUB it shouldn’t try to access files on the partition in question. It’s most often found when booting non-Linux and non-Unix OSs, such as DOS or Windows.

**Chain loader**: The `chainloader +1` line in Listing 1.1 tells the system to load the first sector of the root partition and pass execution to it. This option is common when booting DOS, Windows, or other OSs that place boot loader code in their boot sectors.

**Boot directive**: The `boot` line tells GRUB to actually boot the kernel or boot sector for the OS in this definition. In practice, it can often be omitted.

In order to boot, the GRUB boot loader code must reside in the MBR, the boot partition’s boot sector, or a floppy disk. You can do this by using the `grub` utility, which you launch from a text-mode login or `xterm`:

```bash
# grub
grub> root (hd0,3)
grub> setup (hd0)
grub> quit
```

These commands set the GRUB root partition (the same as the one defined in your `menu.lst` or `grub.conf` file), install the boot loader code to the MBR of the hard disk (that is, to `hd0`), and exit from the utility. If you want to install the boot loader to a partition, you’d use `setup (hd0,3)` or some other partition identifier rather than using `setup (hd0)`. The `grub-install` program provides a simplified method of performing these steps:

```bash
# grub-install (hd0)
```

This command installs GRUB to the MBR of the first disk. It should be able to locate the GRUB root partition automatically.

If you installed a distribution that uses GRUB by default, you shouldn’t have to perform any of these steps; GRUB should already be installed and working. You might need to reinstall GRUB from an emergency boot system if it becomes corrupted, though, and you might want to replace the installed system if you learn of a serious GRUB bug. If you just want to add a new kernel or OS to your existing GRUB installation, you do **not** need to reinstall the boot loader code; you need only edit the `menu.lst` or `grub.conf` file.

## Adding a New Kernel or OS to GRUB

You can add a new kernel or OS to GRUB by copying an existing entry (or using one in Listing 1.1 as a model) and modifying it to suit your needs. When trying a new kernel, don’t replace your old kernel; instead, add the new kernel to the `/boot` directory, and add a description of the new kernel to the GRUB configuration file. Remember to change the `title` line so that you can tell your two kernels apart. When you reboot the computer, you should be able to select the new kernel or OS from the list; there’s no need to reinstall the GRUB boot loader code using the `grub` or `grub-install` tool.

## Naming Kernel Files

A good practice when adding a new kernel is to give it a name that includes its version number or other identifying information. For instance, Listing 1.1’s kernel is called `bzImage-2.6.29`, identifying it as a 2.6.29 kernel. If you had such a kernel and wanted to try adding a new feature (say, XFS support), you might call this new kernel `bzImage-2.6.29-xfs`. There are no hard-and-fast rules for such naming, so use whatever system you like. As a general rule, though, the base of the name begins with `vmlinux` (for a “raw” kernel file), `vmlinuz` (for a kernel compressed with `gzip`), `zImage` (another name for a kernel compressed with `gzip`), or `bzImage` (for a kernel compressed in a way that supports booting larger kernel images). Most distributions use `vmlinuz` for their kernels, but locally compiled kernels usually go by the `bzImage` name.
