
## Configuring and Using CD, DVD, and CD-RW Drives

Linux provides support for using a variety of CD and DVD devices and media. This section shows how to determine what device has been assigned to your CD drive and how to get additional drive information if the drive supports recording on optical media.

AT Attachment Packet Interface, or ATAPI, IDE-based CD drives are recognized during installation and work through the ide-cd kernel module. A symbolic link named /dev/cdrom is created and points to your CD's device (perhaps /dev/hdb or /dev/hdc). You can use many different types of CD drives with Linux, and you can easily replace, add, or upgrade your system to use a new drive. Part of a successful configuration involves the proper installation of the hardware and being able to determine the drive's device when using Linux.

### Checking Drive Assignment

Linux recognizes CD and DVD drives upon booting if they are attached to your computer's motherboard with proper cabling and if they are assigned as either a master or slave on an IDE channel. Look through your kernel boot message for the drive device assignment, such as the following:

```
hdd: DVDROM 10X, ATAPI CD/DVD-ROM drive
```

If you have a DVD-capable drive, you generally should also have a symbolic link named /dev/dvd that points to your drive's device because many DVD clients, such as xine or vlc, look for /dev/dvd by default. If you have a CD-RW drive, the Ubuntu installer inserts a kernel argument into your boot loader's configuration file that specifies use of the ide-scsi kernel, such as the following:

```
append="hdb=ide-scsi"
```

A similar entry in the grub boot loader's /etc/grub.conf file would look like this:

```
kernel boot/vmlinuz-6.5-1.358 ro root=/dev/hda2 hdb=ide-scsi
```

The first CD-RW drive is assigned to the device /dev/scd0 (although it might still be initially recognized while booting as an IDE device), with subsequent drives assigned to /dev/scd1, and so on. To initialize your drive for use, the following modules should be loaded:

| Module | Size | Used by | Not tainted |
|---|---|---|---|
| sg | 30244 | 0 (autoclean) | |
| sr_mod | 15192 | 0 (autoclean) | |
| cdrom | 27872 | 0 (autoclean) | [sr_mod] |
| ide-scsi | 8128 | 0 | |
| scsi_mod | 96572 | 2 [sr_mod ide-scsi] | |

Look for kernel message output regarding the device such as this:

```
Attached scsi CD-ROM sr0 at scsi0, channel 0, id 0, lun 0
sr0: scsi3-mmc drive: 0x/32x writer cd/rw xa/form2 cdda tray
Uniform CD-ROM driver Revision: 3.12
```

Your ATAPI-based CD-RW drive will then work as a SCSI device under emulation, and the symbolic link /dev/cdrom should point to /dev/scd0. You can also use the cdrecord command (included with Ubuntu’s multimedia software packages) to acquire SCSI device information about your drive for later use during the burning operation, as follows:

```
# cdrecord -scanbus
Cdrecord 1.10 (i686-pc-linux-gnu) Copyright (C) 1995-2001 Jörg Schilling
Linux sg driver version: 3.1.22
Using libscg version 'schily-0.5'
scsibus0:
0,0,0     0) 'HL-DT-ST' 'RW/DVD GCC-4120B' '2.01' Removable CD-ROM
0,1,0     1) *
0,2,0     2) *
0,3,0     3) *
0,4,0     4) *
0,5,0     5) *
0,6,0     6) *
0,7,0     7) *
```

The pertinent information—0,0,0 in the example (SCSI bus, device ID, and logical unit number, or LUN)—can then be used during a burn operation like this:

```
# cdrecord -v speed=8 dev=0,0,0 -data -eject file_name.img
```

In this example, a CD-ROM data image named file_name.img is created on a CD-R or CD-RW media at a speed of 8, and the new disk will be ejected after the write operation has completed. See the section “Burning CDs and DVDs in Ubuntu” in Chapter 10, “Multimedia Applications,” for other ways to create CD-ROMs.

### NOTE

Ubuntu also includes the dvdrrecord, dvd+rw-format, and growisofs commands, which can be used with DVD-R and DVD-RW drives.

## Configuring Wireless Networks

Wireless networking used to be a pig to configure for Linux, requiring a lot of complicated steps to connect to a wireless network. However, Ubuntu includes a great utility called Network Manager that makes connecting to and managing wireless networks extremely easy. Thanks to the inclusion of several wireless chipset drivers in the Ubuntu Linux kernel, it is now easy to connect to WEP and WPA encrypted wireless networks.
