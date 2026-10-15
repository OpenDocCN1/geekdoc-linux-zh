
Recent versions of MacOS come on bootable CDs; you can insert the CD and hold down the C key as the computer starts to boot from the CD. These CDs include AppleTalk support, so you can use that to restore files from a backup server, provided that you’ve recovered the files from any secondary storage location you’ve used.

If you have an Iomega Zip drive, you can use the Norton Zip Rescue software available from Iomega (http://www.iomega.com) and bundled with Norton Utilities from Symantec (http://www.symantec.com) to boot a Windows 95 or 98 system. You use this utility to create a boot floppy and minimal Windows installation on a Zip disk. You can then use the Zip Rescue disk set to boot your computer and enable file sharing on the drive you want to recover. You can then perform the restore from Linux, if it was a server-initiated backup. If you initiated the backup from Windows, you need a copy of your backup software on the Zip disk. Unfortunately, there is as yet no version of Norton Zip Rescue for Windows NT, and this utility is tightly tied to Iomega’s Zip drive, so you can’t use it with LS-120 or other removable-media drives.

## Linux Disaster Recovery Floppies

You can create a custom set of Linux boot floppies with support for your network card, SCSI adapter (if present), Samba or NFS, and other minimal tools needed to get a system onto the network. You can then use this boot floppy to restore a system, if the backup was initiated from the Linux backup server. This procedure works whether the client is Linux or Windows, though if you’re using Windows NT, Linux’s preliminary support for NTFS means you might have problems restoring an NTFS system to a fully working state.

Unfortunately, creating the necessary boot floppies for this operation is a challenging task because you need to carefully select the networking software, drivers, and filesystem support you need for your client computers. You might be able to use the Red Hat Linux bootnet.img network install floppy image as a starting point if you elect to try this approach. The bootnet.img file is a floppy image that contains an image file of its own, initrd.img. Although it doesn’t bear a .gz extension, initrd.img is actually gzipped, so you should copy it to the hard disk, rename it initrd.img.gz, and use gunzip to uncompress it. You can then mount it with the Linux loopback driver (as in mount -o loop initrd.img /mnt/floppy) and modify its contents. After you’ve added the utilities you need and deleted those that you don’t need, use gzip to compress the initrd.img file again, rename it, and copy it back to the floppy.

If you prefer, you can create a fuller-featured Linux system on a Zip disk or other removable media, even including X, GUI text editors, and so on. You must install Linux to the removable media, being careful to select only those packages you need. You can then create a boot floppy with DOS, LOADLIN.EXE, and the Linux kernel. Unlike with the Norton Zip Rescue utility for Windows, you can create such emergency Linux disks using LS-120 disks, magneto-optical disks, or other removable-media devices. Although creating an emergency disk setup like this takes some time and planning, it’s easier than creating an emergency boot floppy.

## Tip

If you have a network with several client systems, investing in a removable-media drive to use as an emergency restore system, either using Norton Zip Rescue or a custom Linux installation, is well worth the small cost. Get a portable unit that interfaces via the parallel port for greatest flexibility, or via a SCSI port if many of your systems have SCSI adapters. If you use static IP addresses on your intranet, you can assign one to the emergency restore system. If your hardware varies, you might need to create more than one emergency disk, particularly if you use Norton Zip Rescue.

## Linux Dual Boot

You might want to consider placing a small Linux partition on each client computer. This way, you can boot to Linux to do a complete restore, assuming that the problem is with the client’s filesystem and not a completely trashed hard disk. If the hard disk is trashed, you can restore or reinstall Linux first, and use it to recover the primary client system OS.

## Disk Partition Image Backups

Several programs exist to make "disk image" backups of hard disk partitions. One such program is Drive Image from PowerQuest (http://www.powerquest.com). Upon restoration, these images recover your filesystem almost precisely as it had been before, even including file fragmentation and perhaps filesystem damage. These last two aspects are undesirable, of course, but the basic concept is quite helpful in disaster recovery situations. You need to run the image-creation program, back up the resulting file, and be prepared to restore it later.

If you can boot Linux on the client OS (through a dual-boot setup or emergency boot disk), you can create a disk image backup quite easily by using the Linux dd utility. For instance, suppose you want to create an image of the partition /dev/hda2. You could type

```
dd if=/dev/hda2 of=disk.img
```

The file disk.img now contains a byte-for-byte copy of the contents of /dev/hda2, whether or not Linux understands that filesystem. You can restore the partition by reversing this process. You can also burn the image file to a CD-ROM or copy it to tape.
