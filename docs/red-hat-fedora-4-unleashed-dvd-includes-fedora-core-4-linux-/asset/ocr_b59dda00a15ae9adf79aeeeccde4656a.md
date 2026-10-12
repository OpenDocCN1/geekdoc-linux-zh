vlc, will look for /dev/dvd by default. If you have a CD-RW drive, the Fedora installer will insert a kernel argument into your boot loader's configuration file that specifies use of the ide-scsi kernel. For example,

```
append="hdb=ide-scsi"
```

A similar entry in the grub boot loader's /etc/grub.conf file would look like this:

```
kernel boot/vmlinuz-6.5-1.358 ro root=/dev/hda2 hdb=ide-scsi
```

The first CD-RW drive will be assigned to the device /dev/scd0 (although it might still be initially recognized while booting as an IDE device), with subsequent drives assigned to /dev/scd1, and so on. In order to initialize your drive for use, the following modules should be loaded:

| Module | Size Used by | Not tainted |
|---|---|---|
| sg | 30244 | 0 (autoclean) |
| sr_mod | 15192 | 0 (autoclean) |
| cdrom | 27872 | 0 (autoclean) [sr_mod] |
| ide-scsi | 8128 | 0 |
| scsi_mod | 96572 | 2 [sr_mod ide-scsi] |

Look for kernel message output regarding the device such as this:

```
Attached scsi CD-ROM sr0 at scsi0, channel 0, id 0, lun 0
sr0: scsi3-mmc drive: 0x/32x writer cd/rw xa/form2 cdda tray
Uniform CD-ROM driver Revision: 3.12
```

Your ATAPI-based CD-RW drive will then work as a SCSI device under emulation, and the symbolic link /dev/cdrom should point to /dev/scd0. You can also use the cdrecord command (included with Red Hat's multimedia software packages) to acquire SCSI device information about your drive for later use during burning operation like this:

```
# cdrecord -scanbus
cdrecord 1.10 (i686-pc-linux-gnu) Copyright (C) 1995-2001 Jörg Schilling
Linux sg driver version: 3.1.22
Using libscg version 'schily-0.5'
scsibus0:
	0,0,0   0) 'HL-DT-ST' 'RW/DVD GCC-4120B' '2.01' Removable CD-ROM
	0,1,0   1) *
	0,2,0   2) *
	0,3,0   3) *
	0,4,0   4) *
	0,5,0   5) *
	0,6,0   6) *
	0,7,0   7) *
```