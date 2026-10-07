
![](img/29c52a1767a1e621ce6343faa9399737_49_0.png)

Figure 1.6. pSeries 615 Models 6C3 and 6E3 system design.

## Exploring IBM @serverSeries

capacity, they are placed in a balanced way, with two DIMMs interfacing to each SMI chip.

The electronics complex of the p615 is contained in a compact, unified package. The GX bus provides a four-byte path in each direction for data and addresses to the I/O subsystem. Through the GX bus, the processor and memory are connected to the hot-plug PCI-X slots, the various integrated controllers, the converged service processor (CSP), and backplanes for plugging in disk and media drives. The GX bus provides a bandwidth of 3.2 GBPs, but the aggregate I/O bandwidth through the PCI-X slots is limited to 2 GBPs.

Since the POWER4+ processors are integrated onto the system planner, there is no upgrade from 1-way to 2-way systems, as there are in larger pSeries servers. However, with capacity to accommodate up to 16 GB of memory, almost 1.2 TB of disk storage (8 × 146.8 GB = 1.17 TB), three media drives, and six PCI or PCI-X I/O adapters, the p615 offers excellent flexibility in a UNIX environment.

In addition, the pSeries 615 provides the same features as found in midrange and high-end pSeries servers to ensure high availability. ECC memory with Chipkill and bit steering, hot-swappable disk drive bays, and hot-plug PCI-X slots have already mentioned. The p615 is also designed with redundant hot-plug cooling fans and optionally with redundant hot-plug power supplies. The service processor is integral to the initial boot process and monitors system operations continuously, checking for error conditions. If attached to a modern using Service Agent software, the service processor can notify service personnel in the event of system events that require attention.

With high-performance POWER4+ processors, lots of room to grow in either rack-drawer or deskside configurations, and RAS features that allow even non-technical users to take corrective actions if necessary, the p615 is designed to meet the total computing requirements of small businesses and the needs of large corporations for distributed sites, such as branches or branch offices.

## pSeries 620 Models 6F1 and 6F0 Specifics

The pSeries 620 servers (Figure 1.7) provide significant capacity and processing power in a compact, floor-standing unit that can satisfy all the processing requirements of many small and medium-sized businesses.

## IBM @server pSeries—An Overview

![](img/29c52a1767a1e621ce6343faa9399737_51_0.png)

**Figure 1.7.** pSeries 620 Model 6F0 or 6F1.

The p620-6F0 and p620-6F1 are identical except that Model 6F0 is a 1-, 2- and 4-way SMP, and Model 6F1 also provides a 6-way option. The reason IBM offers two such similar deskside models is that some users need the maximum in expandability in a deskside package (Model 6F1) while others want to take advantage of “workgroup” database pricing (Model 6F0). Workgroup pricing is available in the United States and other countries from vendors like Oracle and IBM on systems with a maximum of 4-way SMP capability. If a system can be expanded above 4-way (even if the customer is not using that capability), then higher enterprise database pricing methods apply. The following description covers both models.

The base configurations of both p620-6F1 and p620-6F0 include the following:

## Exploring IBM @serverSeries

- 1-way 600 MHz RS64 IV processor with 2 MB of L2 cache
- 52 MB of Chipkill memory with ECC
- 18.2 GB SCSI-2 disk drive
- CD-ROM drive
- 1.44 MB 3.5-inch diskette drive
- Built-in service processor
- Integrated I/O ports (do not require use of PCI slots):
- 10/100 Mbps Ethernet
- SCSI-2 (internal) and Ultra2-SCSI (external) ports
- One parallel
- Four serial
- Keyboard
- Mouse
- 2- and 4-way 600 MHz RS64 IV with 4 MB of L2 cache per processor
- 1-, 2- and 4-way 750 MHz RS64 IV with 8 MB of L2 cache per processor
- (Model 6F1 only) 6-way 750 MHz RS64 IV with 8 MB of L2 cache per processor

Memory can be expanded to 32 GB (only to 8 GB in 1-way systems), and storage can be expanded to an impressive 1.0 TB, using both the 12 front-accessible, hot-swappable disk bays and the 12 hot-swappable boot bays. Either SCSI or SSA (Serial System Architecture) backplanes are available. To meet requirements for communications, storage, or other I/O adapters, the p620 models provide 10 hot-plug PCI slots. IBM offers several standard, easy-to-order configurations called p620 Express Configurations to handle Web hosting and database applications.

## pSeries—An Overview

Both the pSeries 620 Model 6F1 and the Model 6F0 offer sufficient scalability in processing power, memory, storage capacity, and I/O capability to handle Supply Chain Management, Enterprise Resource Planning, and Customer Relationship Management. The system architecture of Models 6F1 and 6F0 is shown in Figures 1.8a and 1.8b. In the p620, processor(s) with L1 and L2 caches, and the memory controllers are packaged in a unit called a processor book. This “book” is the physical unit that is exchanged to upgrade from one processor to another or replace a failing processor. The system board for 1-way processor options (Figure 1.8) is a simpler, cost-reduced design that includes some memory DIMM slots on the system board and allows for a memory capacity of 8 GB. The system board for 2-, 4-, and 6-way (Model 6F1 only) options is more complex and allows for the full 32 GB memory capacity on one or two riser cards. As shown in Figure-1.8a, the 6-way configuration of p620-6F1 consists of two cards, a 4-way and a 2-way card. However, this detail does not really matter to the user because the book is the unit installed in the system.

The p620 derives its performance not from fast processors, but also from wide, high-speed buses from processor to memory and to the I/O (RIO) subsystem. The interface from processors to the memory controller is the 16-byte-wide PowerPCXX bus. The interfaces from memory controller to memory DIMMs (labeled SMI bus) are 8 bytes wide, but the bandwidth of the total path from processor to memory controller to memory processors is well matched. For 2-, 4-, and 6-way systems using the RS64 IV port bandwidth is greater than 2 Gbps. Each remote I/O port can operate at 1 Gbps (500 Mbps bidirectional). However, since the second RIO port is used internally as a failover in the event of failures, the theoretical maximum I/O bandwidth is also 1 Gbps (500 Mbps bidirectional). Three PCI bridges drive the 10 PCI slots and integrated Ethernet and SCSI controllers, while an ISA bridge is used for other devices (service processor, diskette, serial and parallel ports, keyboard, mouse).

| | 64-Bit | Bus 7.8 | 64-Bit | 64-Bit | Bus 7.8 | 64-Bit | PCI |
|---|---|---|---|---|---|---|---|
| PCI | 64-Bit | Bus 5.6 | PCI Bridge | PCI 1 | PCI 2 | Bus 5.6 | 64-Bit | PCI |
| PCI | 64-Bit | Bus 3.4 | | | | Bus 3.4 | 5V | PCI |
| PCI | 64-Bit | Bus 1.2 | | | | Bus 1.2 | 64-Bit | 5V | PCI |
| | SCSI 64-Bit | | | | | | | |

![](img/29c52a1767a1e621ce6343faa9399737_54_0.png)

![](img/29c52a1767a1e621ce6343faa9399737_54_1.png)

![](img/29c52a1767a1e621ce6343faa9399737_54_2.png)

**Figure 1.8a.** pSeries 620 Model 6F1 2-, 4-, and 6-way system design (also applies to p620-6F0 2- and 4-way).

| RIO Port 0 | RIO Port 1 |
|---|---|
| SMI Bus 6,7 | 6XX Bus 0 |
| SMI | Memory Controller | 2 MB Cache |
| | | Proc. 1 Way |

1-Way
Mother Board

SMI
Bus 0,1,2,3

| Memory Card 1 |
|---|---|---|---|
| SMI | SMI | SMI | SMI |

**Figure 1.8b.** pSeries 620 Models 6F0 and 6F1 1-way system design.

This design for high performance would really be wasted if equal attention had not been paid to the reliability, availability, and service-ability features of these powerful models. Even though users for the p620-6F1 and p620-6F0 may be moderate-sized businesses, their applications are just as mission-critical as those of very large companies. The pSeries 620 offers a wide range of capabilities that help ensure almost uninterrupted operations.
