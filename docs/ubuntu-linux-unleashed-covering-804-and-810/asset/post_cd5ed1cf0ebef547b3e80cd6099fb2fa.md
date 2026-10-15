
Instructions as described previously. Although you are almost guaranteed to get some error messages, you might at least be able to get a base system running enough to replace files and recover the system.

## TIP

In both preceding cases, it is assumed that you do not need any special file system or device drivers to access the root partition. If you do, add the initrd= argument to the LILO line pointing to the appropriate initrd file on your system. If you do not know the exact name of the initrd file, you are out of luck with LILO, so learn to use a GRUB boot floppy as well.

## Using a GRUB Boot Floppy

The GRand Unified Boot loader (GRUB) can attempt to boot a system from a floppy without a viable custom-made boot floppy. The image for the floppy can be downloaded from ftp://alpha.gnu.org/gnu/grub/grub-0.95-1386-pc.ext2fs and copied to a floppy using dd. (rawrite.exe would be used on a Microsoft system.) Or, if you have a boot floppy from an existing system using GRUB, that one will work as well.

GRUB has its own command shell, file system drivers, and search function (much like command completion in the bash shell). It is possible to boot using the GRUB floppy, examine the drive partitions, and search for the kernel and initrd image as well, using them to boot the system. Worthy of a chapter all its own, the GRUB documentation is extensive: In addition to info grub (the info system is similar to the man system for documentation), the GRUB documents contain a tutorial worth reading. The GRUB boot loader is shown in Figure 13.5.

![](img/8f9e74e2b343ff525bebfb720a3d8441_350_0.png)

FIGURE 13.5 The GRUB boot loader gives you incredible flexibility in booting even unfamiliar systems.

## Using the Recovery Facility

As your computer starts, Ubuntu will show a message prompting you to press Escape to see the GRUB menu. If you do that, you'll see a list of bootable operating systems, which will include Recovery Mode options for your Ubuntu install. If you boot into recovery mode, you'll get automatic root access to your machine which can fix your problems safely.

Alternatively, you can insert your Ubuntu installation disc and use the recovery mode from there. Keep in mind that these recovery modes are designed to be text-only systems for serious system recovery purposes; don't expect them to be hand-held, and don't expect much in the way of ease of use!

## Relevant Ubuntu Commands

The following commands are useful in performing backup, recovery, and restore operations in Ubuntu:

- `amanda`—Amanda is a network-based backup system, consisting of 18 separate commands, for use with Linux.
- `ark`—A KDE desktop GUI archiving utility.
- `cp`—The copy command.
- `scp`—The secure shell copy command.
- `cpio`—A data archive utility.
- `dd`—A data copy and conversion utility.
- `gzip`—The GNU compression utility.
- `tar`—The GNU tape archive utility.

## Reference

- http://www.tldp.org/LDP/solrhe/Securing-Optimizing-Linux-RH-Edition-v1.3/whywhen.html—A thorough discussion with examples of using dump and restore for backups.
- http://en.tldp.org/LDP/solrhe/Securing-Optimizing-Linux-RH-Edition-v1.3/chap29sec306.html—Making automatic backups with `tar` using `cron`.
- http://kmself.home.netcom.com/Linux/FAQs/backups.html—The Linux Backups mini FAQ contains some useful, although brief, comments on backup media, compression, encryption, and security.
- http://www.tldp.org/—The Linux Documentation Project offers several useful HOWTO documents that discuss backups and disk recovery.
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Bootdisk-HOWTO.html#AEN1483—Here is a list of LILO Boot error codes to help you debug a cranky system that will not boot.
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/ftape-HOWTO.html—This is a HOWTO for the floppy tape device driver.
- http://www.linux-usb.org/USB-guide/x498.html—The USB Guide for mass storage devices. If you have a USB device and need to know if it is supported, check here.
- http://www.backupcentral.com/amanda.html—This is the Amanda chapter of Unix Backup and Recovery (written by John R. Jackson and published by O’Reilly and Associates). The chapter is available online and covers every aspect of using Amanda. The site features a handy search tool for the chapter.
- http://twiki.org/cgi-bin/view/Wikilearn/RsyncingALargeFileBeginner—Rsyncing a large file to “repair” a local ISO image that does not pass the md5sum check.
- http://www.lycoris.org/sections.php?op=viewarticle&artid=8—Lycoris ISO rsync mini HOWTO. A step-by-step tutorial on using rsync to sync files.
- http://www.mikerubel.org/computers/rsync_snapshots/—Automated snapshot-style backups using rsync.
- http://www.mondorescue.org/—Mondo Rescue is a bare-metal backup/rescue tool independent of Ubuntu, using CD, DVD, tape, or NFS; it can produce bootable CDs to restore the system.
- http://www.ccp14.ac.uk/ccp14admin/linux-server/mondorescue/dvd_mondo.html—A HOWTO for using MondoRescue to back up on a DVD.
- http://www.linuxorbit.com/modules.php?op=modload&name=Sections&file=index&req=viewarticle&artid=222&page=1—A HOWTO using split and mkisofs to manually back up large archives to CD.
