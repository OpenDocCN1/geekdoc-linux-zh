# Configuring SATA Disks

SATA is a newer interface than PATA, and SATA has largely displaced PATA as the interface of choice. New motherboards typically host four or more SATA interfaces and frequently lack PATA interfaces.

SATA disks connect to their motherboards or controllers on a one-to-one basis—unlike with PATA, you cannot connect more than one disk to a single cable. This simplifies configuration; there aren't jumpers to set, and you won't be concerned with the position of the disk on the cable.

As the word in serial of SATA implies, SATA is a serial bus—only one bit of data can be transferred at a time. SATA transfers more bits per unit of time, though faster than PATA (1.5–6Gbps for SATA vs. 128–1064Mbps for PATA, but these are theoretical maximums that are unlikely to be achieved in real-world situations). Because of SATA's serial nature, SATA cables are much thinner than PATA cables.

Modern firmware detects SATA disks and provides information about them just as for PATA disks. However too, Older BIOSs are likely to be more limited. This is particularly true if your motherboard does not provide SATA support or you use a separate SATA controller card. You may be able to boot from an SATA disk in cases if your controller card supports this, or you may need to use a PATA boot disk.

Most Linux drivers treat SATA disks as if they were SCSI disks, so you should read the next section, "Configuring SCSI disks for information about device naming. Some drivers treat SATA disks like PATA, so you may need to use PATA names in some rare cases.

# Configuring SCSI Disks

There are many types of SCSI definitions, which use a variety of cables and operate at various speeds. SCSI is traditionally a parallel bus, like PATA, although the latest variant, Aerial SCSI (SAS), is a serial bus. SCSI has traditionally considered a superior bus to PATA; however, the cost difference has risen dramatically over the past decade or so, so few people use SCSI on older systems or on very high-end systems.

SCSI supports up to 8 or 16 devices per bus, depending on the variety. One of these is the SCSI host adapter, which is either built into the motherboard or comes as a plug-in card. In practice, the number of devices you can connect to a SCSI bus is much restricted by cable-length limits, which vary from one SCSI variety to another. Each device has its own ID number, typically assigned via a jumper on the device. You must ensure that each device's ID is unique. Consult your documentation to learn how to set the ID.

If your motherboard lacks built-in SCSI ports, others won't want SCSI devices. You can still boot from a SCSI hard disk if your SCSI host adapter has its own firmware that supports booting. Most high-end SCSI host adapters have this support, but low-end SCSI host adapters don't. If you use such an adapter, you can still attach SCSI hard disks to the adapter, and Linux can use them, but you will need to boot from a PATA or SATA hard disk.