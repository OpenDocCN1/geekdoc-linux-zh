
v4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

## Examining the Physical Media

Now we are ready to start collecting information. One of the things we'll need to do is re-inventory our system's connected devices to ensure we identify the correct subject. Normally you would have taken notes on the physical markings of the hard drive (or other media) as you would have removed it from the source computer, etc. Use an enlarged photocopy of the disk label as part of acquisition notes, providing a reliable record of identification.

In this particular case, I will be using a USB to SATA bridge. Because there is some translation, I want to make sure I can identify the bridge as well as the disk attached to it. Once the bridge is attached and powered on, I can run ls to see its information. If you are using a directly attached SATA drive, you will not need to run this command:

```
root@forensic1:~# ls
Bus 006 Device 002: ID 8087:0024 Intel Corp. Integrated Hub
Bus 002 Device 007: ID 2109:0812 VIA Labs, Inc. VL818 Hub
Bus 002 Device 012: ID 174C:0516 ASMedia Technology Inc. ASM105 SATA bridge
Bus 002 Device 006: ID 2109:0812 VIA Labs, Inc. VL818 Hub
```

So knowing we are dealing with a 40GB hard disk (ST340014AS) on USB/SATA bridge (ASMedia Technology), we can identify its device node with ls:

```
root@forensic1:~# ls
[0:0:0] disk INTEL SSD2CT1200 /dev/sda
[0:0:0] disk Hitachi HDS7230A5C /dev/sdb
[0:0:0] cdrom HL-ST24NS001 /dev/sr0
[0:0:0] disk Generic Compact Flash /dev/ide
[0:0:0] disk Generic SM /dev/sdf
[0:0:0] disk Generic SD /dev/sdg
[0:0:0] disk Generic MS-Pro /dev/sdh
[0:0:0] disk ASMT21050 /dev/sdc
```

In this case, the drive itself is not identified because ls is querying the kernel sysfs for hosts attached to the system. It is not sending queries to that. Now we can query the disk attached to the host using hdparm. In this case the bridge supports SATA translation, so commands pass through to the drive itself. This tool can provide detailed information as well as powerful commands to set options on a disk. Some of these options are used for forensic examiners. First, however, we are looking for information. For that we can use the simple hdparm with the -I option on our subject disk, /dev/sd. This gives detailed information about the disk that we can record to a file:

```
root@forensic1:~# hdparm -I /dev/sdc

/dev/sdc
ATA device, with removable media
Model Number: ST340014AS
Serial Number: 5M00QS22
Firmware Revision: 8.12

Standards:
Used: ATA/ATAPI-6 T13 1410 version 2
Supported: 6 5 4

Configuration:
Logical max current
cylinders 16383 16383
heads 16 16
sectors/track 63 63

CHS current address sectors: 16514064
LBA user address sectors: 78125000
LBA48 user address sectors: 78125000
Logical/Physical Sector size: 512 bytes
device size with M=1024*1024: 38146 MBytes
device size with M=1000*1000: 40000 MBytes (40 GB)
cache/buffer size = 2048 KBytes

Capabilities:
LBA, IORDY (can be disabled)

Queue depth: 32
Standby time values: spec'd by Standard, no device specific minimum
R/W multiple sector transfer: Max = 16 Current = ?nRecommended account management value: 128, current value: 0

DMA: dma udma0 udma1 udma2 udma3 udma4 udma5 udma6
Cycle time: min120ns recommended=120ns
PIO: pio0 pio1 pio2 pio3
Cycle time: no flow control=240ns IORDY flow control=120ns

Commands/features:
Enabled:
- SMART feature set
- Security Mode feature set
- Power Management feature set
- Write cache
- Look-ahead
- Host Protected Area feature set
- WRITE_BUFFER command
- READ_BUFFER command
- SMART feature set
- Native Command Queuing (NCQ)
- Security enabled
- Configuration: C
- Firmware: 8.12
- Date code: 0530
- Code: WU![](img/99364c785d6888a5ade02ca808d_93.png)

In this particular case, I will be using USB to SATA bridge. Because there is some translation going on, I want to make sure I can identify the bridge as well as the disk attached to it. Once the bridge is attached and powered on, I can run ls to see its information (for emphasis). If you are using a directly attached SATA drive, you will not need to run this command:

So knowing we are dealing with a 40GB hard disk (ST340014AS) on USB/SATA bridge (ASMedia Technology), we can identify its device node with ls:

- Configuration: C

Some of these options are used for forensic examiners. First, however, we are looking for information. For that we can use the simple hdparm with the -I option on our subject disk, /dev/sd. This gives detailed information about the disk the drive itself is not identified because ls is querying the kernel sysfs for hosts attached to the system. It is not sending queries to that. Now we can query the disk attached to the host using hdparm. In this case the bridge supports SATA translation, so commands pass through to the drive itself. This tool can provide detailed information as well as powerful commands to set options on a disk. Some of these options are used for forensic examiners. First, however, we are looking for information. For that we can use the simple hdparm with the -I option on our subject disk, /dev/sd. This gives detailed information about the disk that we can record to a file:

- Configuration: C
- Firmware: 8.12
- Date code: 0530
- Code: WU

Some of these options are used for forensic examiners. First, however, we are looking for information. For that we can use the simple hdparm with the -I option on our subject disk, /dev/sd. This gives detailed information about the disk that we can record to a file:

- Configuration: C
- Firmware: 8.12
- Date code: 0530
- Code: WU
