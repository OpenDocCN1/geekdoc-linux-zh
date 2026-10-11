# # EIDE Versus SCSI Disks

One of the biggest debates concerning hard disks is that between proponents of *Enhanced Integrated Device Electronics* (EIDE) drives and those who favor *Small Computer Systems Interface* (SCSI) devices. All modern x86 motherboards include EIDE controllers, but to attach a SCSI drive, you must normally purchase a separate SCSI host adapter (see Chapter 9 for more information on SCSI host purchases). Each technology has its advantages and disadvantages, and I describe these in this section.

# **NOTE**

The terms *EIDE*, *Advanced Technology Attachment* (ATA), and *ATA Packet Interface* (ATAPI) refer to closely interrelated technologies, as does *Integrated Device Electronics* (IDE). As a general rule, *IDE* and *EIDE* refer to hard disks, whereas *ATA* and *ATAPI* refer to non-disk devices. *ATA* is sometimes used in conjunction with a number to describe the revision number of the ATA interface, as in *ATA-2* (ATA revision 2) or *ATA/33* (a 33Mbps version of ATA).

# ## EIDE Controllers

Because EIDE controllers are built in to all modern motherboards, it’s important to pick a motherboard that supports the fastest form of EIDE possible. The interfaces you’re most likely to see in the motherboards of 2000 are 33Mbps and 66Mbps variants. These variants can be referred to in various ways—for instance, a 33Mbps EIDE interface can be referred to as *ATA/33*, *Ultra-33*, or *UltraDMA 33*.

# ## The History of EIDE

IDE was EIDE’s predecessor in the marketplace, and EIDE is, as the name implies, an enhancement to IDE. IDE, in turn, was a successor to older hard disk technologies. These older technologies used hard disks with very little electronic circuitry in conjunction with a separate interface board. IDE integrated these two components into one, hence the name. From the motherboard’s point of view, an IDE controller looks just like a controller for an older drive type.

As late as the mid-1990s, plain IDE drives were quite common. IDE controllers from this period and earlier used a method of control known as *programmed input/output* (PIO), in which the computer’s CPU fetched every byte transferred to or from the hard disk. PIO mode