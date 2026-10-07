used with pSeries systems attach to Small Computer System Interface
I/O controller circuitry.

# SCSI Disk Storage

SCSI (pronounced "scuzzy") is an industry-standard way of connecting
devices (disks, tape, CD-ROM drives, etc.) to computer systems. The
SCSI controller circuitry (often more than one controller) resides on the
system board in all pSeries systems or on the I/O driver backplane.
Depending on the system configuration and application requirements,
SCSI storage devices are often attached via a SCSI adapter card plugged
to into a PCI or PCI-X slot. In either case, the SCSI controller circuitry is
built around a microprocessor specially programmed to implement the
SCSI protocol.

Figure 1.33 shows how devices are attached to the SCSI I/O con-
Each SCSI-compatible device is attached to a shared cable or bus
a daisy-chain fashion. Up to 15 SCSI devices can share a single
current SCSI bus. The original SCSI buses support up to eight devices.
In addition to the SCSI I/O controller, these devices can be a single disk
unit, a single tape unit, or a controller with up to other device
attached. To improve system performance, however, it is better to place

![](bbox=[0.19, 0.555, 0.85, 0.866])

**Figure 1.33.** Devices are attached to the SCSI controller via a daisy-chained
cable scheme.