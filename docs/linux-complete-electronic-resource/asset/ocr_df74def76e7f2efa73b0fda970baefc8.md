solation options available to Linux users: software RAID, outboard DASD boxes, and RAID disk controllers.

**Software RAID** Pure software RAID implements the various RAID levels in the kernel disk (block device) code.

**Outboard DASD Solutions** DASD (Direct Access Storage Device) are separate boxes that come with their own power supply, provide a cabinet/chassis for holding the hard drives, and appear to Linux as just another SCSI device. In many ways, these offer the most robust RAID solution.

**RAID Disk Controllers** Disk Controllers are adapter cards that plug into the ISA/EISA/PCI bus. Just like regular disk controller cards, a cable attaches them to the disk drives. Unlike regular disk controllers, the RAID controllers will implement RAID on the card itself, performing all necessary operations to provide various RAID levels.

Related HOWTOs can be found at:

+   http://MetaLab.unc.edu/mdw/HOWTO/mini/DPT-Hardware-RAID.html

+   http://MetaLab.unc.edu/mdw/HOWTO/Root-RAID-HOWTO.html

+   http://MetaLab.unc.edu/mdw/HOWTO/mini/Software-RAID.html

RAID at Linas.org:

+   http://linas.org/linux/raid.html

# # Redundant Networking

**IP Address Takeover (IPAT)** When a network adapter card fails, its IP address should be taken by a working network card in the same node or in another node.

**MAC Address Takeover** When an IP takeover occurs, it should be made sure that all the nodes in the network update their ARP caches (the mapping between IP and MAC addresses).