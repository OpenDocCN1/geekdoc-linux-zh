Any hardware made after about 1998 is designed to work in UDMA mode, and you won't have to worry about a thing if you have these four components:

+   - A hard disk that supports Ultra DMA mode
+   - An 80-pin IDE cable
+   - A motherboard (or IDE controller) that supports Ultra DMA mode
+   - Support in the operating system (or BIOS) for Ultra DMA mode

If you're missing any one of these items, your system will still run but in a reduced-speed mode, generally one of the PIO modes natively supported in the BIOS. Motherboards or controllers that don't support UDMA might prove troublesome. Issues with instability and lockups caused by controller issues can usually be solved either by upgrading the BIOS (to enable the controller to support UDMA) or by disabling UDMA in the disk itself through software utilities available from the manufacturer of the disk. These utilities typically run only under DOS or Windows and are either included with the disk or downloadable from the manufacturer's Web site.

FreeBSD fully supports Ultra DMA, making it perhaps the strongest link in this chain; you can see whether all the necessary components are present by watching the device-probing messages during boot (or using dmesg afterwards):

```
ad0: 6194MB <HITACHI_DK239A-65> [13424/15/63] at ata0-master using UDMA33
```

If the UDMA capability isn't detected and the hard disk is new but the rest of the machine's components aren't, you should find the disk manufacturer's drive management utility, boot the system from an MS-DOS floppy, and use the utility to disable the disk's UDMA capability. This will keep you running at a lower speed than the disk can go, but it's for the best. The alternative is to run the risk of crashes and lockups. Your system will thank you for not pushing it beyond its means.

# SCSI Disks

If all this IDE nonsense is something you can afford to bypass, or if you will be attaching external disks to your system, your alternative is SCSI. At first glance, the litany of SCSI modes, shown in Table 18.4, looks hardly any less bizarre than that of IDE.

TABLE 18.4 SCSI Transfer Modes

| Standard | Transfer Mode | Transfer Speed | Max Cable Length | Devices/IDs | Connector |
| :--- | :--- | :--- | :--- | :--- | :--- |
| SCSI-1 | SCSI | 5 MBps | 6m | 8 | 50-pin |
| SCSI-2 | Fast SCSI | 10 MBps | 3m | 8 | 50-pin |
| | Wide SCSI | 10 MBps | 6m | 16 | 68-pin |
| | Fast Wide SCSI | 20 MBps | 3m | 16 | 68-pin |