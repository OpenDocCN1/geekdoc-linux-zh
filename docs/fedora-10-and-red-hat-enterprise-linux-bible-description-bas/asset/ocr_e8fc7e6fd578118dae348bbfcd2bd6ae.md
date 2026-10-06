# Chapter 13: Backing Up and Restoring Files 547

| | | |
| 0,0,2 | 2) * |
| 0,0,3 | 3) * |
| 0,0,4 | 4) * |
| 0,0,5 | 5) * |
| 0,0,6 | 6) * |
| 0,0,7 | 7) * |

This tells you that the CD drive is using SCSI ID zero. The Logical Unit Number in this case should always be zero, so you now have all three numbers. You supply them to crecord as part of the dev parameter.

The SCSI bus number is listed first; it is followed by the ID, and then the LUN. The entire command should look similar to this:

```
# crecord -v speed=2 dev=0,0,0 -data /var/tmp/mary.iso
```

For an ATAPI CD drive, the CD drive as /dev/cdrom, your command line might appear as follows instead:

```
# crecord -v speed=2 dev=/dev/cdrom -data /var/tmp/mary.iso
```

Several parameters are included in the command. The -v parameter tells crecord to supply verbose output to what speed at (in this case X2). (You might choose to leave off speed=2 and let crecord autodetect the record speed of your CD burner). The -data parameter tells crecord to burn WAV or AU files as data, instead of audio tracks. Without that option, file types are burned as audio tracks while all other files are burned as data.

Before running crecord live, you might consider adding the -dummy option, which runs through the CD burn process without actually touching the laser. You can add the -ject parameter to eject the CD when it is done. As it works, crecord will display status messages like to the following:

```
crecord: No write mode specified.
crecord: Assuming -tao mode.
crecord: Future versions of crecord may have drive dependent defaults.
crecord-Clone 2.01-dev (i686-pc-linux-gnu) Copyright (C) 1995-2004 Jörg
Schilling
TOC type: 1 = CD-ROM
scsisdev: '/dev/cdrom'
devname: '/dev/cdrom'
scsibus: -2 target: -2
Warning: Open by 'devname' is unintentional and not supported.
Linux sg driver version: 3.5.27
Using libsg version 'schily-0.8'
SCSI buffer size: 64512
atapi: 1
Device type : Removable CD-ROM
```