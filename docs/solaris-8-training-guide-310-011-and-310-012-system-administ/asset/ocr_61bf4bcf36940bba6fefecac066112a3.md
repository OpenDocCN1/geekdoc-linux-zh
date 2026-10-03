Use the probe-scsi command to obtain a free open SCSI target ID number before adding a tape unit, CD-ROM drive, disk drive, or any other SCSI peripheral. Only devices that are powered on will be located, so make sure that everything is turned on. Use this command after installing a SCSI device to ensure that it has been connected properly and that the system can see it. Also, use this command if you suspect a faulty cable or connection. If you have more than one SCSI bus, use the probe-scsi-all command.

The following examples use some of the diagnostic features of OpenBoot. The first example uses probe-scsi to identify all the SCSI devices attached to a particular SCSI bus. This command is useful for identifying SCSI target IDs that are already in use, or to check to make sure that all devices are connected and identified by the system.

```
ok probe-scsi
```

The system will respond with this:

```
Target 1
    Unit 0  Disk      SEAGATE ST1120N 833400093849
    Copyright   1992 Seagate
    All rights reserved 0000
Target 3
    Unit 0  Disk  MAXTOR LXT-213S SUN2074.20
```

This example uses the probe-ide command to identify all IDE devices connected to the PCI bus:

```
ok probe-ide
    Device 0 ( Primary Master )
        ATA Model: ST34321A
    Device 1 ( Primary Slave )
        Not Present
    Device 2 ( Secondary Master )
        Removable ATAPI Model: CRD-8322B
    Device 3 ( Secondary Slave )
        Not Present
```

The next example tests the system video and performs various other tests:

```
ok test all
```

To test the disk drive to determine whether it is functioning properly, put a formatted, high-density disk into the drive and type the following:

```
ok test floppy
```

The system should respond with this:

```
Testing floppy disk system. A formatted disk should be in the drive.
Test succeeded.
```