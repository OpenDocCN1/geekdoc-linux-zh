
floppy disk, CD-ROM, or other disk devices, depending on the BIOS's capabilities and configuration) for a small boot loader program. This program normally resides on the master boot record (MBR) of a hard disk or the boot sector of a floppy disk. The MBR resides on the first sector of a hard disk and controls the boot process. A boot sector is the first sector of a floppy or of a hard disk partition and also controls the boot process. (In the case of a partition's boot sector, it's used after the MBR.)

> The BIOS, as it currently exists, is extremely old and limited. A new system, known as the Extensible Firmware Interface (EFI), is poised to replace the BIOS. Intel-based Macintoshes already use EFI, as do a few other systems; however, EFI is not yet common on commodity PCs. If your system uses EFI, its boot process will differ from that described here.

In the case of a PC that runs nothing but Windows, the boot loader in the MBR is hard-coded to check for a secondary boot loader in the active primary partition—that is, a partition that's been marked as holding a bootable OS. This secondary boot loader directly loads the Windows kernel. The approach in Linux is similar, but standard Linux boot loaders are more complex. The Linux Loader (LILO) and the Grand Unified Boot-loader (GRUB) are the most common Linux boot loaders. Both programs enable you to boot the Linux kernel or to redirect the boot process to another OS.

In some cases, a system uses multiple boot loaders. One resides in the MBR, and another resides in the boot sector of an individual disk partition. (OSs on different partitions can each have their own boot sector-based boot loaders.) In this configuration, the MBR-based boot loader is the primary boot loader, and the one in a partition's boot sector is a *secondary boot loader*. Some boot loaders work in only one of these positions. It's often possible for a secondary boot loader to redirect the boot process to a different partition, in which case that partition's boot loader becomes the tertiary boot loader, although the configuration is the same as for secondary status.

## Available Boot Loaders

Many OSs ship with their own boot loaders, and others are available from third parties. These are some of the most common boot loaders:

- **LILO**
  This boot loader can directly boot a Linux kernel, and it can function as either a primary or a secondary boot loader. It may also be installed on a floppy disk. LILO can redirect the boot process to non-Linux partitions, and so it can be used to select Linux or Windows in a dual-boot system. Although once very popular, LILO has been largely eclipsed by GRUB as the boot loader of choice for Linux.

- **GRUB**
  This boot loader is more or less the standard Linux boot loader. GRUB can be installed in the same locations as LILO—a floppy disk, the MBR, or the boot sector of a Linux partition. It can directly load the Linux kernel, as well as some other OS kernels, or it can redirect the boot process to another boot loader to load other OSs, such as Windows.

## Configuring Boot Loaders

**OS Loader** This is one name by which Windows NT/2000/XP/Vista’s boot loader goes. Another is **NTLDR**. This is a secondary boot loader that cannot directly boot Linux, but it can boot a disk file that can contain LILO or GRUB and hence boot Linux indirectly. It’s common on some dual-boot installations.

**LOADLIN** This is an unusual boot loader in that it’s neither a primary nor a secondary boot loader. Rather, it’s a DOS program that can be used to boot Linux after DOS has already loaded. It’s particularly useful for emergency situations because it enables you to boot a Linux kernel using a DOS boot floppy, and you can also use it to pass kernel parameters to influence the booted system’s behavior. **LOADLIN** comes with most Linux distributions, generally in a directory on the main installation CD-ROM.

Many additional third-party boot loaders are available, most of which cannot directly boot a Linux kernel but can boot a partition on which LILO or GRUB is installed. For this reason, this chapter emphasizes configuring **GRUB**—this boot loader can be used to boot Linux, whether it functions as the primary, secondary, or tertiary boot loader. If you opt to use GRUB as a secondary boot loader, you’ll need to consult the documentation for your primary boot loader to learn how to configure it.

![](img/a78bc63f22351f522ba5ec1fa0c060d2_48_0.png)

> On a Linux-only system, there’s no need to deal with a third-party boot loader; LILO or GRUB can function as a primary boot loader without trouble on such systems. Third-party boot loaders are most useful when you have two or more OSs installed and particularly when LILO or GRUB has trouble redirecting the boot process to the other OSs, which is rare.

The usual configuration for GRUB is to place it in the MBR. Even in a Linux-only situation, however, it’s sometimes desirable to place GRUB in the Linux boot partition. Used in this way, a standard DOS/Windows MBR will boot Linux if the Linux boot partition is a primary partition that’s marked as active. This configuration can be particularly helpful in Windows/Linux dual-boot configurations because Windows tends to overwrite the MBR at installation. Therefore, putting GRUB in the Linux boot sector keeps it out of harm’s way, and you can get GRUB working after installing or reinstalling DOS or Windows by using the DOS or Windows FDISK program and marking the Linux partition as active. If GRUB is on the MBR and is wiped out, you’ll need to boot Linux in some other way, such as by using **LOADLIN**, and then rerun grub-install to restore GRUB to the MBR.

## Configuring GRUB

GRUB is a collection of several components, including the boot loader code proper, a configuration file, and a set of utilities for installing and manipulating the boot loader code. The boot loader code can read the configuration file, so there’s no need to reinstall the boot loader code whenever you change your GRUB configuration. You can even place the configuration file on a non-Linux partition, which can be handy for quickly reconfiguring GRUB from another OS.

GRUB wasn’t developed exclusively for Linux. It can be installed from, and used to boot, a wide variety of OSs. Its Web page is http://www.gnu.org/software/grub. Most Linux distributions use GRUB Legacy (version 0.97 or earlier). GRUB 2 is currently in development.

## Real World Scenario

### The 1024-Cylinder Limit

One bane of the PC world that reared its ugly head twice in the 1990s was the so-called 1024-cylinder limit. This limit is derived from the fact that the x86 BIOS uses a three-number scheme for addressing hard disk sectors. Each sector is identified by a cylinder number, a head number, and a sector number, known collectively as the sector’s CHS address. The problem is that each of these values is limited in size. The cylinder number, in particular, is allotted only 10 bits and so cannot exceed 2¹⁰, or 1,024, values. In conjunction with the limits for sectors and heads, this restricted addressable ATA hard disk size to 504MB in the early 1990s.

When disks larger than 504MB became common, BIOSes were adjusted with CHS translation schemes, which allowed them to juggle numbers between cylinders, heads, and sectors. This increased the limit to just under 8GB. A similar scheme abandoned CHS addressing for BIOS-to-disk communications but retained it for BIOS-to-software communications. This was known as linear block addressing (LBA) mode.

These limits never affected Linux once it had booted, because Linux could handle more than 10-bit cylinder values, and it could access disks directly using LBA mode. The Linux boot process was limited, however, because LILO (this was pre-GRUB) relied on CHS addressing via the BIOS to boot the kernel. Therefore, the Linux kernel has traditionally had to reside below the 1,024-cylinder mark.

Today, all new BIOSs include support for so-called extended INT13 calls, which bypass the CHS addressing scheme. These BIOSs support booting an OS from past the 1,024-cylinder mark on a hard disk, but only if the boot loader and OS support this feature. Recent versions of LILO and GRUB support extended INT13 calls, so new Linux distributions can be installed anywhere on a hard disk—if the BIOS supports this feature.

### Setting Global GRUB Options

The traditional location for the GRUB configuration file is /boot/grub/menu.lst. Fedora, Gentoo, and Red Hat, though, ship with a version of GRUB that uses /boot/grub/grub.conf as the configuration file. Whatever the name, the GRUB configuration file has the same basic form, as illustrated in Listing 1.1.
