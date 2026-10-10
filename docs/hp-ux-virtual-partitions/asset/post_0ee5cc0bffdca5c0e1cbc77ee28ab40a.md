
## Appendix B

### Superdome Virtual Partitions

### Superdome vPars

At the time this book is going to press, I have been working with the very first prerelease vPars software for Superdome. This appendix contains salient information related to vPars on Superdome based on my preliminary work. All of the material covered throughout this book applies to vPars on Superdome. The hardware paths of Superdome are substantially different from those on the L-Class and N-Class systems used in the examples throughout this book. I will, therefore, cover some brief examples of vPars on Superdome that include path-related information.

Each Superdome hard partition (nPartition) is the equivalent of a separate server. The examples of L-Class and N-Class systems that are used throughout this book are like a Superdome nPartition. We can, therefore, load several vPars on each nPartition provided that we meet all the requirements for vPars at the time of this writing, such as:
- a separate boot device for each vPar;
- each Local Bus Adapter (LBA) assigned to only one vPar;
- a minimum of one CPU per vPar; and so on.

For the upcoming example, we have indeed met these requirements.

The Guardian Service Processor (GSP) on the Superdome is used to supply console control for the Superdome complex. By connecting to the GSP, you can select the nPartition that will have console control. You can switch the console control to any of the nPartitions in the Superdome complex. This is different from the Ctrl-A function we use to switch the console between vPars. When we connect to our nPartition using the console through the GSP, we are connected to the nPartition, not to one of the vPars within the nPartition. As part of the configuration of vPars in an nPartition, we will assign the core I/O card to one of the four vPars in our nPartition.

Let's begin our Superdome vPar work by viewing a complete Superdome complex and then focusing on one nPartition that will be used to support multiple vPars.

### The Hierarchy of Partitions

Figure B-1 shows the hierarchy of partitions on our Superdome complex:

![](img/eff8b9287a5f38c5adf538f24aacf29e_1019_0.png)

**Figure B-1 Multiple vPars within nPartitions in a Superdome Complex**

Each nPartition can contain multiple vPars. nPar3 of the nPartitions in Figure B-1 is expanded to show that it will run four Virtual Partitions in our upcoming example.

Let’s now move on to view the hardware in the nPartition in which we’ll create our vPars.

### nPartition and Superdome Background

nPartitions are hard partitions within a Superdome platform. A Superdome server can support anywhere from one to 16 nPartitions, each supporting its own operating system, applications, peripherals, and networks. Currently, each nPartition can host HP-UX operating environments. When the Intel IPF versions of Superdome are available, nPartitions will support Linux and Windows environments as well. There are currently two nPartitions supported on an rp8400.

Superdome is based on a modular set of components. The system is built on a cell-based hierarchical crossbar architecture that can be configured as one large symmetric multiprocessor or as several independent partitions. A cell, or cell board, is the basic building block of the Superdome system; it is a symmetric multiprocessor (SMP), containing up to four processors and up to 16 GBytes of main memory.

At their core, nPartitions support a user-defined partitioning of resources and isolate hardware and software errors. A Superdome nPartition consists of one or more cells that communicate over a high-bandwidth, low-latency crossbar fabric. Cells are grouped into physical structures called *cabinets* or *nodes*. Special programmable hardware in the cells defines the boundaries of a partition in such a way that isolation is enforced from the actions of other partitions. Each partition runs its own independent operating system. Different partitions may be executing different versions of the operating system. In the future, when Itanium Processor Family (IPF) CPUs are supported, different operating systems, such as HP-UX, Linux, and Windows, will be supported simultaneously in different partitions.

Each partition has its own CPUs, memory, and I/O resources, consisting of the resources of the cells that make up the partition. Resources may be removed from one partition and added to another without having to physically manipulate the hardware, just by using commands that are part of the system’s management interface. Additionally, dynamic additions of new nPartitions are supported. Adding or removing cell boards to or from existing nPartitions does not affect other partitions.

### Working with nPartitions and vPars

To assign the components that will be assigned to the vPars within an nPartition, you must run ioscans in the nPartition in which the vPars will be created. This provides a list of all I/O components, CPUs, and so on, available in the nPartition to be used in the vPars. The ioscans does not show components in the other nPartitions. The following full ioscans listing shows all the components in the nPartition in which we'll create our four vPars:

```
# ioscans -f

Class I H/W Path Driver S/W State H/W Type Description
-----------------------------------------
root 0 root CLAIMED BUS_NEXUS
cell 0 5 cell CLAIMED BUS_NEXUS
10a 0 5/0 sba CLAIMED sba System
Bus Adapter (804) 0 5/0/0 iba CLAIMED BUS_NEXUS Local PCI
ba 0 5/0/0 iba CLAIMED BUS_NEXUS Local PCI
Bus Adapter (782) 0 5/0/0/0 abso0 CLAIMED INTERFACE PCI
c1 0 5/0/0/0/0 abso0 CLAIMED INTERFACE PCI
Serial (102c1c843) 0 5/0/0/1/0 btlam CLAIMED INTERFACE HP PCI
lan 0 5/0/0/1/0 btlam CLAIMED INTERFACE HP PCI
10/100Base-TX Core 1 5/0/1 iba CLAIMED BUS_NEXUS Local PCI
ba 1 5/0/1 iba CLAIMED BUS_NEXUS Local PCI
Bus Adapter (782) 0 5/0/1/0/0 c720 CLAIMED INTERFACE SCSI C695
ext_bus 0 5/0/1/0/0 c720 CLAIMED INTERFACE SCSI C695
Fast Wide LVD 0 5/0/1/0/0 tgt CLAIMED DEVICE
larget 0 5/0/1/0/0 tgt CLAIMED DEVICE SEAGATE
disk 0 5/0/1/0/0 tgt CLAIMED DEVICE SEAGATE
ST318404LC 1 5/0/1/0/1 tgt CLAIMED DEVICE
target 1 5/0/1/0/1.0 tgt CLAIMED DEVICE
disk 1 5/0/1/0/1.0 dsdsk CLAIMED DEVICE HP
73_4G013734G5JC 1 5/0/1/0/2 acll CLAIMED DEVICE
targets 2 5/0/1/0/2 tgt CLAIMED DEVICE
targets 2 5/0/1/0/2 tgt CLAIMED DEVICE
ctl1 0 5/0/1/0/0.7.0 act1 CLAIMED DEVICE Initiator
targets 3 5/0/1/0/0.15.0 tgt CLAIMED DEVICE
ctl1 1 5/0/1/0/0.15.0 accl1 CLAIMED DEVICE HP
AS4Z72A 2 5/0/2 lba CLAIMED BUS_NEXUS Local PCI
ba 2 5/0/2 lba CLAIMED BUS_NEXUS Local PCI
Bus Adapter (782) 1 5/0/2/0/0 PcltoPcl CLAIMED BUS_NEXUS PCltoPcl
ba 1 5/0/2/0/0 PcltoPcl CLAIMED BUS_NEXUS PCltoPcl
Bridge 1 5/0/2/0/0/4/0 btlam CLAIMED INTERFACE HP AS5506B
lan 1 5/0/2/0/0/4/0 btlam CLAIMED INTERFACE HP AS5506B
PCI 10/100Base-TX 4 Port 2 5/0/2/0/0/5/0 btlm CLAIMED INTERFACE HP A5506B
PCI 10/100Base-TX 4 Port 3 5/0/2/0/0/5/0 btlm CLAIMED INTERFACE HP A5506B
lan 3 5/0/2/0/0/5/0 btlm CLAIMED INTERFACE HP A5506B
PCI 10/100Base-TX 4 Port 4 5/0/2/0/0/5/0 btlm CLAIMED INTERFACE HP A5506B
PCI 10/100Base-TX 4 Port 4 5/0/2 lba CLAIMED BUS_NEXUS Local PCI
Bus Adapter (782) 5 5/0/3/0/0 PcItoPcI CLAIMED BUS_NEXUS PcItoPcI
Bridge 5 5/0/3/0/0 btlm CLAIMED INTERFACE HP A5506B
lan 5 5/0/3/0/0/4/0 btlm CLAIMED INTERFACE HP A5506B
PCI 10/100Base-TX 4 Port lan 6 5/0/3/0/0/5/0 btlm CLAIMED INTERFACE HP A5506B
PCI 10/100Base-TX 4 Port lan 7 5/0/3/0/0/6/0 btlm CLAIMED INTERFACE HP A5506B
PCI 10/100Base-TX 4 Port lan 8 5/0/3/0/0/7/0 btlm CLAIMED INTERFACE HP A5506B
PCI 10/100Base-TX 4 Port lan 8 5/0/4 lba CLAIMED BUS_NEXUS Local PCI
Bus Adapter (782) 6 5/0/4 c720 CLAIMED INTERFACE SCSI C895
ext_bus Fast Wide LVD target disk 5/0/4/0/0.0 5/0/4/0/0.1 c720 CLAIMED DEVICE
sdaa
ST18144LC target disk 5/0/4/0/1.1 sdisk CLAIMED DEVICE HP
73.4G5T5334GSLC 5/0/4/0/0.7 tgct CLAIMED DEVICE
ctel 2 5/0/4/0/0.7.0 accl CLAIMED DEVICE Initiator
target 7 5/0/4/0/0.15 tgct CLAIMED DEVICE
ctel 3 5/0/4/0/0.15.0 accl CLAIMED DEVICE HP
A5272A ba 7 5/6 lba CLAIMED BUS_NEXUS Local PCI
Bus Adapter (781) ext_bus 2 5/6/0/0.0 c720 CLAIMED INTERFACE SCSI C895
Fast Wide LVD target 8 5/6/0/0.0 tgct CLAIMED DEVICE
disk 8 5/6/0/0.0 sdaak CLAIMED DEVICE SEAGATE
ST131844LC target disk 9 5/6/0/1.0 tgct CLAIMED DEVICE
sdial 5/6/0/0.1.0 73.4G5T5334GSLC target disk 10 5/6/0/0.2 sdaik CLAIMED DEVICE HP
73.4G5T5374GSLC 5/6/0/0.2.0 target 11 5/6/0/0.7 tgct CLAIMED DEVICE
ctel 4 5/6/0/0.7.0 accl CLAIMED DEVICE Initiator
target 12 5/6/0/0.15 tgct CLAIMED DEVICE
ctel 5 5/6/0/0.15.0 accl CLAIMED DEVICE HP
A5272A ba 8 5/0/8 lba CLAIMED BUS_NEXUS Local PCI
Bus Adapter (782) fc 9 5/0/9/0/0.0 td CLAIMED INTERFACE HP
Tachyon TL/TS Fibre Channel Mass Storage Adapter 11 5/0/9/0/0.8 fcpp CLAIMED INTERFACE FCP
Protocol Adapter ba 9 5/0/9 lba CLAIMED BUS_NEXUS Local PCI
Bus Adapter (781) ba 10 5/0/9/0/0 PcItoPcI CLAIMED BUS_NEXUS PcItoPcI
Bridge lan 9 5/0/9/0/4/0 btlm CLAIMED INTERFACE HP A5506B
PCI 10/100Base-TX 4 Port lan 10 5/0/9/0/4/0/5/0 btlm CLAIMED INTERFACE HP A5506B
PCI 10/100Base-TX 4 Port lan 11 5/0/9/0/0/6/0 btlm CLAIMED INTERFACE HP A5506B
PCI 10/100Base-TX 4 Port lan 12 5/0/9/0/0/7/0 btlm CLAIMED INTERFACE HP A5506B
PCI 10/100Base-TX 4 Port ba 11 5/0/10 lba CLAIMED BUS_NEXUS Local PCI
Bus Adapter (782) fc 11 5/0/10/0.0 td CLAIMED INTERFACE HP
Tachyon TL/TS Fibre Channel Mass Storage Adapter fcpp 1 5/0/10/0.0.8 fcpp CLAIMED INTERFACE FCP
```
