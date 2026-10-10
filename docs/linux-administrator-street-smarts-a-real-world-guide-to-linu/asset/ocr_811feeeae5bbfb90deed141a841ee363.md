version number of the Linux driver that's responsible for the drive). You can examine these files by using `cat` or `less`:

```
$ cat /proc/ide/hda/driver
ide-disk version 1.188
```

![](bbox=[0.15, 0.24, 0.27, 0.31])

> Although most of the pseudo-files in the /proc/ide directory tree are world-readable, some are not; you must be root to access these pseudo-files.

Although the /proc/ide directory tree provides useful information, it's not always the best way to learn about your disk devices. One good alternative is the hdparm utility, which enables you to read or set various hard disk options. To obtain a summary of information on your drive, use the -i option as root

```
# hdparm -i /dev/hda

/dev/hda:
```

Model=WDC WD600AB-32BVAO, FwRev=21.01H21, SerialNo=WD-WMA7E1272684
Config={ HardSect NotMFM HdSw>15uSec SpinMotC1 Fixed DTR>5Mbs FmtGapRef }
RawCHS=16383/16/63, TrkSize=57600, SectSize=600, ECCbytes=40
BuffType=DualPortCache, BuffSize=2048kB, MaxMultSect=16, MultSect=off
CurCHS=4047/16/255, CurSects=16511760, LBA=yes, LBASects=117231408
IORDy=on/off, tPIO={min:120,w/IORDy:120}, tDMA={min:120,rec:120}
PIO modes: pio0 pio1 pio2 pio3 pio4
DMA modes: mdma0 mdma1 mdma2
UDMA modes: udma0 udma1 udma2 udma3 udma4 *udma5
AdvancedPM=no WriteCache=enabled
Drive conforms to: Unspecified: ATA/ATAPI-1 ATA/ATAPI-2 ATA/ATAPI-3
ATA/ATAPI-4 ATA/ATAPI-5

* signifies the current active mode

This command returns a wide range of basic information, including the drive's model, firmware revision, serial number, cylinder/head/sector (CHS) counts, buffer size, access modes supported (PIO, DMA, and UDMA), and more. Even if most of this information is like Greek to you, having a record of it should be useful, so save it to a file or print it for future reference.
Unfortunately, both the /proc/ide directory tree and hdparm are useful only for PATA drives or for SATA drives that are managed by drivers in the PATA section of the Linux kernel. For SCSI drives and SATA drives that are handled by drivers in the SCSI section of the Linux kernel, less information is available through these methods. There is a /proc/scsi directory tree, but its contents are more concerned with the SCSI host adapter than with the devices it handles.