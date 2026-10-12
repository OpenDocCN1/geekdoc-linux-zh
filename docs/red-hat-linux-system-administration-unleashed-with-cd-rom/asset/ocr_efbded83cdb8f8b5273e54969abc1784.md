**Table 10.3 continued**

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
Cdrecord release 1.8a17 Copyright 1995-1998 Jrg Schilling
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
Cdrecord release 1.8a17 Copyright 1995-1998 Jrg Schilling
TOC Type: 1 = CD-ROM
scsidev: '2,0'
scsibus: 0 target: 2 lun: 0
atapi: 0
```