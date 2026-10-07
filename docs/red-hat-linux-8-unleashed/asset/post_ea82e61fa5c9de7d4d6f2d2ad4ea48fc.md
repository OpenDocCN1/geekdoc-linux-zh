
# CHAPTER 11 Backing Up, Restoring, and Recovery

## Booting the System from a Generic Floppy

If you failed to make a boot floppy or cannot locate the one you made, any Linux boot floppy (a slightly older version or one borrowed from a friend) can be pressed into service as it has a reasonably similar kernel version. (The major and minor numbers—for example, 2.4.13 would likely work with any 2.4 system, but not with a 2.2 system.) You would boot your system by manually specifying the root and boot partitions described previously. Although you are almost guaranteed to get some error messages, you might at least be able to get a base system running enough to replace files and recover the system.

## Special Drivers

In both proceeding cases, it is assumed that you don't need any filesystem or device drivers to access the root partition. If you do, add the initrd= argument to the LILO line. If you don't know the exact name of the initrd file, you are out of luck with LILO, so learn to use a GRUB floppy as well.

## Using a GRUB Boot Floppy

The Grand Unified Bootloader (GRUB) can be a lifesaver when attempting to boot a system from a floppy with a viable custom-made boot floppy. The image for the floppy can be downloaded from ftp://alpha.gnu.org/gnu/grub/grub-0.90-i386-pc.ext2fs and copied to a floppy using dd. (write.exe would be used on a Microsoft system.) Or, if you have a boot floppy from an existing system using GRUB, that one will work as well.

> NOTE
> It seems that alpha.gnu.org has been offline. A temporary location for the files has been established at http://www.gnu.org/software/grub/grub-download.html.

GRUB has its own shell, filesystem drivers, and function search (much like command completion in the bash shell). It is possible to boot using the GRUB floppy, examine the drive partitions, and search for the kernel and initrd image as well, using them to boot the system. Worthy of a chapter all its own, the GRUB documentation is extensive: In addition to info GRUB (the info system is similar to the man system for documentation), the GRUB documents contain a tutorial worth reading. The flexibility and power of GRUB are influenced by Red Hat to make the default bootloader for Red Hat Linux.

![](img/446debe023486a07fde575245cf7a3ff_388_0.png)
FIGURE 11.5 The GRUB bootloader gives you incredible flexibility in booting unfamiliar systems.

## Using the Recovery Facility from the Installation Disk

As in the previous example, the linux rescue command at the boot prompt to launch the CD in rescue mode. Rescue mode runs a version of Red Hat from the CD-ROM that is independent from your system. It permits you to mount your root partition for maintenance. This is useful when your root partition is no longer bootable because something has gone wrong. Red Hat is constantly improving the features of the Recovery Facility.

Upon beginning the rescue mode, you get your choice of language and keyboard layouts. The minimal operating system attempts to mount your Red Hat installation at /mnt/sysimage; this step can be skipped (you might not want to mount anything yet), and it will drop you to command shell.

If you choose to mount the installation, you are asked to confirm which partition is the root partition. The rescue function also offers support for software RAID arrays (RAID 0, 1, and 5), as well as IDE or SCSI partitions formatted as ext2, ext3, reiserfs, vfat, fat, and mdfs. After asking for input if it is unsure how to proceed, you eventually arrive at a command shell; there is no login or password. Depending on your configuration, you might or might not see prompts for additional information.

If you need connectivity, the ne2k-pci and 8390 modules are available as the ifconfig, route, rcp, login, rsh, and ftp commands. For archiving (restoring archives), cpio, uncpio, gzip, gunzip, dd, zcat, and md5sum commands are there. For editors, vi and pico are also available as other useful system commands. A closer look at these commands reveals that they are all links to a program called busybox (home page at http://busybox.lineo.com/).

BusyBox provides a reasonably complete POSIX environment for any small or embedded system. The utilities in BusyBox generally have fewer options than their full-featured GNU cousins; however, the included options "provide the expected functionality and behave very much like their GNU counterparts." This means that you should test the rescue mode to see if you can restore your data and see which options are available to you because the BusyBox version will behave slightly differently from the full GNU version. (Some options are missing; some options don't quite work the same—you to know if this will affect you before you are in an emergency situation.)

## Alternatives to the Red Hat Rescue CD

The Red Hat rescue CD might be inadequate for your system restoration needs; it might lack Ethernet support, filesystem support, or the kind of full utility functionality that you require for a successful recovery. An alternative exists in the SuperRescue CD created by H. Peter Anvin.

Essentially, SuperRescue CD is a reasonably full and robust Red Hat distribution (based on Red Hat 7.2 and the 2.4.18-preac3 kernel) that runs completely from the CD. The best thing about SuperRescue CD is that it comes with scripts, so it is incredibly easy to use.

## Relevant Red Hat and Linux Commands

The following commands are useful in backup, recovery, and restore:

- amdump: Amanda is a network-based backup system.
- cp: The secure copy command.
- scp: The secure shell command.
- cpio: A data archive utility.
- dd: A data copy and conversion utility.
- gzip: The GNU compression utility.
- tar: The GNU archive utility.

## Reference

http://www.tldp.org/HOWTO/Filesystems-HOWTO.html: The Filesystems HOWTO is a good place to start if you are dealing with an unfamiliar filesystem.

http://www.tldp.org/Bootdisk-HOWTO/index.html: The Linux Bootdisk HOWTO covers the design and construction of boot. It will find a great deal of information about the boot process, providing background information to assist you in solving problems.

http://www.tldp.org/Bootdisk-HOWTO/a1439.html: Here’s a list of LILO Boot code to help you debug a cranky system that won’t boot.

http://metalab.unc.edu/pub/Linux/system/boot/lilo/lilo-u-21.gz: If it isn’t installed on system and you cannot find the CD to this is the LILO User Documentation.

http://www.freshmeat.net: The Freshmeat site serves a steady stream of Linux announcements and information, as well as providing a search function for the site.

http://www.google.com/linux/: The Linux-specific section of Google helps eliminate less-useful hints.

http://kmself1.home.net.com/Linux/FAQs/backups.html: The Linux Backups-FAQ contains some useful, although brief, comments on backup media, encryption, and security.

http://www.tldp.org: The Linux Documentation Project offers several useful HOWTO documents that discuss backups and disk recovery.

http://www.tldp.org/mini/Ext2fs-Undeletion.html: If you need to delete a file from an ext2/3 filesystem, the Ext2fs Undeletion mini-HOWTO is the document for you. You will be successful if you practice.

http://www.tldp.org/mini/Ext2fs-Undeletion-Dir-Struct/index.html: The Ext2fs Undeletion Directory Structures is a companion HOWTO to the Linux Ext2fs mini-HOWTO, helping you cope with an errant rm -rf *.

http://www.tldp.org/FAQ/Ftape-FAQ.html: This is a FAQ for the floppy tape device driver; it’s a little old.

http://www.linux-usb.org/USB-guide/x498.html: The USB Guide for mass storage devices. If you have a USB device and need to know if it’s supported, check here.
