```
# iname ieee1394
# loaded ocel1394
```

Next, look for relevant device information from the linux kernel using the dmesg command:

```
ohci1394: S$Revision: 1.00 $ Ben Collins <bcollins@debian.org>
PCI: Found IRQ 10 for device 00:0b.0
PCI: Sharing IRQ 10 with 00:07.5
ohci1394-0: [002-0] 1.0 (PCI: [R0=] [WIO= [ee000000 ee000080)] \
        Max Packet=[2048]
ieee1394: Device added: node 2:1023, GUID 000010500007d8e
ieee1394: sbp2: Driver forced to serialize I/O (serialize_io = 1)
ieee1394: sbp2: Node 2:1023: Max speed [S400] - Max payload [2048]
SCSI: IEEE-1394 SBP-2 protolcol driver
        Vendor: TEAC  Model: CD-W28E       Rev: 1.1A
        Type:  CD-ROM                 ANSI SCSI revision: 02
```

In this example, the FireWire drivers have recognized a CD-RW drive (which will be assigned to /dev/sc07 because another CD-RW is also present on the system). You might also find that the sbp2 kernel module has loaded:

```
Module                  Size Used by  Not tainted
sb p2                 14400  0
ohci1394               15872  0 (unseqd)
ieee1394               25760  0 [sbp2 ohci1394]
```

> Fedora’s installer should recognize any FireWire hardware in your PC during installation.
> Depending on your computer’s hardware, you might find an entry in /etc/mcdprobe.conf such as alias ieee1394-controller ohci1394.

Again, use the cdrecord command and its -scansbus option to obtain information needed to use the drive under SCSI emulation:

```
# cdrecord -scansbus
cdrecodr 1.10 (i686-pc-linux-gnu) Copyright (C) 1995-2001 Jörg Schilling
Linux sg driver version: 3.1.22
Using libscg version 'schily-0.5'
scsiibus0:
    0,0,0  0) 'HL-DT-ST' 'RW/DVD GCC-4120B' '2.01' Removable CD-ROM
    0,1,0  1) *
    0,2,0  2) *
    0,3,0  3) *
    0,4,0  4) *
```