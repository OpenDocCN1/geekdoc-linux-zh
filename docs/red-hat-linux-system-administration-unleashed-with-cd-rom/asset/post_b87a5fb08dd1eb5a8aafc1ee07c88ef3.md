
```
27061 extents written (52 Mb)

[root@madmax linux-2.2.5]# mount -t iso9660 -o loop=/dev/loop0,ro ../ksource.img /mnt/cdrom

[root@madmax linux-2.2.5]# cd /mnt/cdrom

[root@madmax cdrom]# ls -a
.  MAINTAINERS  Rules.make  include  mm
..  Makefile  arch  init  modules
COPYING  README  drivers  ipc  net
CREDITS  README.kernel.sources  fs  kernel  pcmcia-cs-3.0.9
Documentation  REPORTING-BUGS  ibcs  lib  scripts

[root@madmax cdrom]# cd

[root@madmax /root]# umount /mnt/cdrom
```

As you can see, the long filenames in the kernel source tree were converted to the 8.3 format specified by the ISO9660 standard. However, since we specified the -r option and Linux supports the Rock Ridge extensions to ISO9660, when the image is mounted the filenames show up just like in the original source tree. It is usually a good idea to mount the image you create to verify that the filesystem image is properly created. You can do this by using the loop device and the loop option to the mount command. Another interesting option was the multiple -m options used to exclude object files, library archives, and other files that would be present if you had built a kernel in the source tree.

Now that an image has been created, you can use either the cdwrite or cdrecord command to transfer the image to the CD-R or CD-RW media. Of these commands, only cdrecord is included on the Red Hat installation media. The decision on which of these two commands to use is up to you, and is dependent on support for hardware and other features that you may require. Please note that cdrecord is being actively maintained and that cdwrite is not. If there is not a specific feature that you need that is only supported in cdwrite, I recommend that you stick with cdrecord. These packages are available from the following FTP sites if you want to build them from the source, or from the Red Hat contrib mirrors if you prefer prebuilt binaries:

ftp://ftp.fokus.gmd.de/pub/unix/cdrecord/ (cdrecord)
ftp://sunsite.unc.edu/pub/Linux/utils/disk-management/ (cdwrite)

Be sure to get the appropriate command to support your hardware. For purposes of our example, we will use the cdrecord command because it supports ATAPI as well as SCSI devices. The cdrecord command supports a large number of command-line options, and some of the most common are described in Table 10.3. The option type indicates where on the command line the options may appear. The general options must all be specified before any track options or track filenames.

## TABLE 10.3 cdrecord Command-Line Options

| Option | Type | Description |
|---|---|---|
| -version | General | Prints out the cdrecord version info and exits. |
| -v | General | increases the general verbosity level by 1. |
| -V | General | increases the SCSI command transport verbosity by 1. |
| -debug | General | Prints additional debugging messages. |
| -dummy | General | Goes through all steps of burning with the laser off. |
| -multi | General | Allows multisession CDs to be made. This option must be used for all sessions of the disk except the last. |
| -msinfo | General | Retrieves multisession info in a format suitable for the mkisofs command to use with the -c option. |
| -toc | General | Displays the table of contents or PMA info for a CD. |
| -fix | General | Fixates the disk only. |
| -nofix | General | Does not fixate a disk. Used to create an audio disk in steps. |
| speed=# | General | Sets the speed factor for the writing process to #. |
| blank=type | General | Blanks a CD-RW disk and exits or blanks the disk before writing. To obtain a list of blanking types, set type equal to help. |
| dev=target | General | Writes to device specified by target. The format of target is devicename:scsibus, scsid, lun. This may be shortened to those parts required to uniquely identify the drive. (Example: dev=0,2,0 for Bus 0, ID 2, Lun 0) |
| -checkdrive | General | Checks if a driver for the current drive is present and exits. An exit status of 0 indicates success. |
| -scanbus | General | Displays the inquiry strings for all SCSI devices on the bus. |
| -inq | General | Displays the device inquiry info and exits. |

### Table 10.3 continued

| Option | Type | Description |
|---|---|---|
| -prcap | General | Displays the drive capabilities for SCSI-3/ mmc drives. |
| -audio | Track | All subsequent tracks are written to disk in CD-DA audio format. |
| -data | Track | All subsequent tracks are written to disk in CD-ROM mode 1 format. |
| -mode2, -xa1, -xa2, -cdi | Track | All subsequent tracks are written to disk in the specified format (CD-ROM mode 2, CD-ROM XA mode 1, CD-ROM XA mode 2, or CDI format). |
| -swab | Track | Assumes audio data is in byte-swapped (little-endian) order. |
| -isosize | Track | Uses the ISO9660 filesystem size as the size of the next track. |

To continue our example, we will now write the image we created with mkisofs to a CD-R disk using cdrecord. It is a good idea to do this when the machine is relatively idle, due to the sensitivity of the burning process. This process requires a constant stream of data and if load on the device bus or system load interrupts this stream, a buffer underrun will occur. Then the disk being written will be useless, unless you happen to be creating a mobile or like-gold coasters. Following is a sample of the command to write our ISO9660 image to disk and then to mount and verify that the write was successful.

```
[root@wizard src]# cdrecord -scanbus
Cdrecord release 1.8a17 Copyright 1995-1998 Jörg Schilling
scsibus0:
0) *
1) *
2) * 'CD-R/RW RW7040S ' '1.10' Removable CD-ROM
3) *
4) *
5) *
6) *
7) *
```

```
[root@wizard src]# cdrecord -dummy -v -isosize speed=4 dev=2,0 ksource.img
Cdrecord release 1.8a17 Copyright 1995-1998 Jörg Schilling
TOC Type: 1 = CD-ROM
scsidev: '2,0'
scsibus: 0 target: 2 lun: 0
atapi: 0
```

```
Device type : Removable CD-ROM
Version : 2
Response Format: 2
Capabilities :
Vendor_info :
Identifikation : 'CD-R/RW RW7040S '
Revision : '1.10'
Device seems to be: Generic mmc CD-RW.
Using generic SCSI-3/mmc CD-R driver (mmc_cdr).
Driver flags : SWABAUDIO
Track 01: data 52 MB
Total size: 60 MB (06:00.84) = 27063 sectors
Lout start: 61 MB (06:02/63) = 27063 sectors
Current Secsize: 2048
ATIP info from disk:
Indicated writing power: 4
Is not unrestricted
Is not erasable
ATIP start of lead in: 23276 (15:39/01)
ATIP start of lead out: 72226 (116:05/01)
Disk type unknown
Manufacturer unknown (not in table)
Blocks total: 333226 Blocks current: 333226 Blocks remaining: 306163
Starting to write CD/DVD at speed 4 in dummy mode for single session.
Last chance to quit, starting dummy write in 1 seconds.
Waiting for reader process to fill input-buffer ... input-buffer ready.
Starting new track at sector: 0
Track 01: Track 01: 52 of 52 MB written (fifo 100%).
Track 01: Total bytes read/written: 55420928/55420928 (27061 sectors).
Writing time: 93.369s
Fixating...
WARNING: Some drives don't like fixation in dummy mode.
Fixating time: 0.013s
cdrecord: fifo had 1602 puts and 1692 gets.
cdrecord: fifo was 0 times empty and 1530 times full, min fill was 96%.
```

```
[root@wizard src]# cdrecord -v -isosize speed=4 dev=2,0 ksource.img
Cdrecord release 1.8a17 Copyright 1995-1998 Jörg Schilling
TOC Type: 1 = CD-ROM
scsidev: '2,0'
scsibus: 0 target: 2 lun: 0
atapi: 0
Device type : Removable CD-ROM
```

```
Version : 2
Response Format: 2
Capabilities :
Vendor_info :
Identifikation : 'CD-R/RW RW7040S '
Revision : '1.10'
ATIP info from disk:
Indicated writing power: 4
Is not unrestricted
Is not erasable
ATIP start of lead in: 23276 (15:39/01)
ATIP start of lead out: 72226 (116:05/01)
Disk type unknown
Manufacturer unknown (not in table)
Blocks total: 333226 Blocks current: 306013 Blocks remaining: 278956
Starting to write CD/DVD at speed 4 in write mode for single session.
Last chance to quit, starting real write in 1 seconds.
Waiting for reader process to fill input-buffer ... input-buffer ready.
Starting new track at sector: 0
Track 01: 52 of 52 MB written (fifo 100%).
Track 01: Total bytes read/written: 55420928/55420928 (27061 sectors).
Writing time: 94.725s
Fixating...
Fixating time: 61.882s
cdrecord: fifo had 1692 puts and 1692 gets.
cdrecord: fifo was 0 times empty and 1473 times full, min fill was 94%.
```

```
[root@wizard src]# mount -t iso9660 /dev/scd0 /mnt/cdrom
mount: block device /dev/scd0 is write-protected, mounting read-only

[root@wizard src]# cd /mnt/cdrom

[root@wizard cdrom]# ls
COPYING README drivers ipc net
CREDITS README.kernel-sources fs kernel pcmcia-cs-3.0.9
Documentation REPORTING-BUGS ibcs lib scripts
MAINTAINERS Rules.make include mm
Makefile arch init modules

[root@wizard src]# umount /mnt/cdrom

[root@wizard src]# eject scd0
```
