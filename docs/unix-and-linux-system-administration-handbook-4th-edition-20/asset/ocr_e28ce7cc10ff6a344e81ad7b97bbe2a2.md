# Chapter 8 Storage

The traditional parallel ATA interface (PATA) connected disks to the motherboard with a 40- or 80-conductor ribbon cable. This style of disk is nearly obsolete, but the installed base is enormous. PATA disks are often labeled "IDE" to distinguish them from SATA drives (below), but they are true ATA drives. PATA disks are medium to fast speed, generous in capacity, and unbelievably cheap.

+   - ATA, SATA, is the successor to PATA. In supporting much higher transfer rates (currently 3 Gb/s, with 6 Gb/s soon to arrive), SATA simplifies connectivity with tidier cabling and a maximum cable length. SATA has native support for hot-swapping and (optional) command queuing, two features that finally make ATA a viable alternative to SCSI in server environments.

+   - Not as common as it once was, SCSI is one of the most widely supported disk interfaces. It comes in several flavors, all of which support multiple disks on a bus and various speeds and communication styles. SCSI is described in more detail on page 216.

Hard drive manufacturers typically reserve SCSI interfaces for their highest-performing and most rugged drives. You'll pay more for these drives, but mostly because of the drive features rather than the interface.

+   - Fibre is a serial interface that is popular in the enterprise thanks to its high bandwidth and to the large number of storage devices that can be attached to it or. Fibre devices connect with a fiber optic or twinaxial copper cable. Speeds range from 1–40 Gb/s depending on the protocol revision.

Common topologies include loops, called Fibre Channel Arbitrated Loops (FC-AL), and fabrics, which are constructed with Fibre Channel switches. Fibre Channel can connect several protocols, including SCSI and IP. Devices are identified by a hardwired, 8-bit ID number (a "World Wide Name") that's similar to an Ethernet MAC address.

+   - The Universal Serial Bus (USB) and FireWire (IEEE1394) serial communication systems have become popular for connecting external hard disks. Current speeds are 480 MB/s for USB and 800 MB/s for FireWire; both systems are too slow to accommodate a fast disk streaming data at full speed. Upcoming revisions of both standards will offer more competitive speeds (up to 5 Gb/s with USB 3.0).

Hard disks never provide native USB or FireWire interfaces—SATA controllers are built into the disk enclosures that feature these ports.

ATA and SCSI are by far the dominant players in the disk drive area. They are the only interfaces we discuss in detail.