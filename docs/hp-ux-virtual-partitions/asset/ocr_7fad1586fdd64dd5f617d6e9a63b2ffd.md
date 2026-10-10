![](bbox=[0.18, 0.15, 0.93, 0.54])

Figure 11-28 Disk Devices Window

The first two entries refer to internal disks in an L-Class system. The third entry is a CD-ROM drive. Let's compare this output to what we would see when we run ioscans:

```
$ /usr/sbin/ioscan -funcC disk

Class I /H/W Path Driver S/W State H/W Type Description
-----------------------------------
disk 1 0/0/1/1.2.0 sdisk CLAIMED DEVICE SEAGATE ST318203LC
/dev/dsk/c1t2d0
/dev/rdsk/c1t2d0
disk 2 0/0/2/0.2.0 sdisk CLAIMED DEVICE SEAGATE ST318203LC
/dev/dsk/c2t2d0
/dev/rdsk/c2t2d0
disk 3 0/0/2/1.4.0 sdisk CLAIMED DEVICE TOSHIBA CD-ROM XM-6201TA
/dev/dsk/c314d0
/dev/rdsk/c314d0
```