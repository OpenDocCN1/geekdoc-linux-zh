# Which is better, SCSI or SATA?

# Serial SCSI

As in the PATA world, parallel SCSI is giving way to Serial Attached SCSI (SAS), the SCSI analog of SATA. From the hardware perspective, SAS improves just every aspect of traditional parallel SCSI.

+   Chained buses are passe. Like SATA, SAS is a point-to-point system. SAS allows the use of "expanders" to connect multiple devices to a single host port. They're analogous to SATA port multipliers, whereas support for port multipliers is hit or miss, expanders are always supported.

+   SAS does not use terminators.

+   SCSI target IDs are no longer used. Instead, each SAS device has a Fibre-Channel-style 64-bit World Wide Name (WWN) assigned by the manufacturer. Analogous to an Ethernet MAC address.

+   The number of devices in a SCSI bus "SAS domain," really is no longer limited to 8 or 16. Up to 13,384 devices can be connected.

SAS currently operates at 3 Gb/s, but speeds are scheduled to increase to 6 Gb/s and then 12 Gb/s by 2012.

# Which is better, SCSI or SATA?

In past editions of this book, SCSI was the obvious interface choice for server applications. It offered the highest available bandwidth, out-of-order command execution (aka tagged command queueing), lower CPU utilization, easier handling of many storage devices, and access to the market's most advanced drives.

The advent of SATA has removed or minimized most of these advantages, SCSI simply not deliver the bang for the buck that it used to. SAS drives competes with (and in some cases, outperform) equivalent SCSI disks in nearly every category. At the same time, both SATA devices and the interfaces and cabling to them are cheaper and far wider available.

SCSI still has a few trump cards:

+   Manufacturers continue to use the SATA/SCSI divide to stratify the market. To help justify premium pricing, the fastest and most reliable drives are still available with only SCSI interfaces.

+   SAS is limited to a queue depth of 32 pending operations. SCSI can handle thousands.

+   SAS can handle many storage devices (hundreds or thousands) on a single host. But keep in mind that all devices share a single pipe to the host; you are still limited to 3 Gb/s of aggregate bandwidth.

The SAS vs. SATA debate may ultimately be most because because the SAS standard includes support for SATA drives. SAS and SATA connectors are similar enough