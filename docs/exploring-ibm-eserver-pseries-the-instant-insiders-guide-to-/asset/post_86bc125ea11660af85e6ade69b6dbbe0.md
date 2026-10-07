
# IBM @serverSeries—An Overview

systems, however, their physical architecture is quite different from that of the corresponding p620 models. IBM also offers standard, easy-to-order configurations called p660-6H0 and p660-6H1 Express Configurations, which are analogous to the p620 Express Configurations.

The processor options for p660-6H1 and p660-6H0 are the same as in p660-6F1 and p660-6F0:

- 1-way 600 MHz RS64 IV with 2 MB of L2 cache
- 2- and 4-way 600 MHz RS64 IV with 4 MB of L2 cache per processor
- 1-, 2-, and 4-way 750 MHz RS64 IV with 8 MB of L2 cache per processor
- (Model 6H1 only) 6-way 750 MHz RS64 IV with 8 MB of L2 cache per processor

Therefore, some electronics architecture and memory bandwidth as discussed for the pSeries 620 (Figure 1.8a and 1.8b) apply to Models 6H1 and 6H0, which offer the same maximum memory of 32 GB (8 GB maximum on 1-way systems) as Models 6F1 and 6F0. Memory on all p660 servers uses IBM's Chipkill technology, which corrects double bit-errors, and in the event of a high error rate, the offending section of memory off-line and logs a service action message for the system administrator to schedule when convenient.

Beyond the processor and memory architecture, the physical packaging and I/O capability of the p660 servers differ from those of the p620 tower servers. These rack-mountable servers consist of a 5 CEC drawer (Figure 1.15) with processors, memory, and the surrounding system logic, plus one or two I/O drawers, also 5U high. Primary I/O drawer (Figure 1.16) is required, so a base system is 10U (17.5 inches) high. Another way to look at it is that one can package up to three Model 6H1 or 6H0 systems in the 36U-high Model T00 rack for maximum density of systems on available floor space. If a second I/O drawer is needed or other devices, such as storage subsystems, are required, perhaps only one or two p660-6H1 or p660-6H0 servers will occupy a rack.

Models 6H1 and 6H0 require a primary I/O drawer and may optionally use a second I/O drawer for further expansion. The interface

![](img/29c52a1767a1e621ce6343faa9399737_78_0.png)

**Figure 1.15.** pSeries 660 Model 6H0 or 6H1 processor drawer.

![](img/29c52a1767a1e621ce6343faa9399737_78_1.png)

**Figure 1.16.** pSeries 660 I/O drawer, used in Models 6H0, 6H1, and 6M1.

Exploring IBM @server pSeries

The interface from the processor complex (DEC drawer) to the I/O drawer is composed of two RIO (remote I/O) ports (see Figures 1.8a and 1.8b), connected in a loop. Each RIO port has an aggregate bandwidth of 1 Gbps (500 MBps bidirectional). With one I/O drawer, the overall bandwidth is 1 Gbps (just as for the p620 models), but with two I/O drawers, transmissions to each drawer are sent from the CEC by the path to each drawer and the overall bandwidth is doubled, to 2 Gbps. In the event of a failure in one of the RIO ports, all traffic is routed on the working port. Although the bandwidth falls back to 1 Gbps, the system continues to run.

The primary I/O drawer features two integrated SCSI controllers (SCSI-2 F/W [fast/wide] internal and Ultra2-SCSI external), an Ethernet 100 controller, four slots and one parallel path, keyboard and mouse ports. In addition, the I/O drawer includes 14 hot-plug PCI slots (four 32-bit and ten 64-bit), which allow for addition or removal of adapter cards when the system is running, and three media bays. Two of the media bays are filled by default with a CD-ROM drive and a diskette drive. The third is available and is used most for a tape drive. With the CEC, a redundancy option is available for the hot-plug supplies and cooling fans in the I/O drawer. This I/O drawer is also used on the pSeries 660 660M1.

Since the I/O drawers do not provide disk bays

The pSeries 660 Models 6H1 and 6H0 are powered by 220-volt AC power, or alternatively, for the special needs of the telecommunications industry, by 48 volts DC. Also, for telecommunications central office or other environments with harsh operating conditions, these systems are designed for NEBS Level 3 compliance.

With their highly reliable and scalable design and performance (roughly twice that of the pSeries 640), the p660-6H1 and p660-6H0 servers are targeted at the key commercial processing segments of e-business: enterprise resource planning, supply chain management, and business intelligence. They are often used as application servers in a three-tiered system design—database application on one system, application server on the second (the p660 servers, in this example), and end-user workstations as the third layer.

## pSeries 660 Model 6M1 Specifics

The pSeries 660 Model 6M1 is a very powerful and scalable member of the 64-bit family of SMP enterprise servers. Positioned above the Models 6H1 and 6H0, the p660-6M1 provides the power, capacity, and expandability needed for mission-critical applications.

The Model 6M1 provides excellent midrange performance for transaction processing (TPC-C), Web serving (Specweb99), and server-side Java application processing (Specjb29). The p660-6M1 derives its power from two, four, six, or eight RS64 IV 750 MHz processors with 8 MB of L2 cache. For entry-level configurations, two or four RS64 III 500 MHz processors with 4 MB of L2 cache are available.

The pSeries 660 Model 6M1 is a very powerful and scalable member of the 64-bit family of SMP enterprise servers. The drawers consist of a 5 CEC drawer (Figure 1.15) with processors, memory, and the surrounding system logic, plus one or two I/O drawers, also 5U high. Primary I/O drawer (Figure 1.16) is required, so a base system is 10U (17.5 inches) high. Another way to look at it is that one can package up to three Model 6H1 or 6H0 systems in the 36U-high Model T00 rack for maximum density of systems on available floor space. If a second I/O drawer is needed or other devices, such as storage subsystems, are required, perhaps only one or two p660-6H1 or p660-6H0 servers will occupy a rack.

Models 6H1 and 6H0 require a primary I/O drawer and may optionally use a second I/O drawer for further expansion. The I/O drawer features two integrated SCSI controllers (SCSI-2 F/W [fast/wide] internal and Ultra2-SCSI external), an Ethernet 100 controller, four slots and one parallel path, keyboard and mouse ports. In addition, the I/O drawer includes 14 hot-plug PCI slots (four 32-bit and ten 64-bit), which allow for addition or removal of adapter cards when the system is running, and three media bays. Two of the media bays are filled by default with a CD-ROM drive and a diskette drive. The third is available and is used most for a tape drive. With the CEC, a redundancy option is available for the hot-plug supplies and cooling fans in the I/O drawer. This I/O drawer is also used on the pSeries 660 660M1.

Since the I/O drawers do not provide disk bays

The pSeries 660 Models 6H1 and 6H0 are powered by 220-volt AC power, or alternatively, for the special needs of the telecommunications industry, by 48 volts DC. Also, for telecommunications central office or other environments with harsh operating conditions, these systems are designed for NEBS Level 3 compliance.

With their highly reliable and scalable design and performance (roughly twice that of the pSeries 640), the p660-6H1 and p660-6H0 servers are targeted at the key commercial processing segments of e-business: enterprise resource planning, supply chain management, and business intelligence. They are often used as application servers in a three-tiered system design—database application on one system, application server on the second (the p660 servers, in this example), and end-user workstations as the third layer.

## pSeries 660 Model 6M1 Specifics

The pSeries 660 Model 6M1 is a very powerful and scalable member of the 64-bit family of SMP enterprise servers. Positioned above the Models 6H1 and 6H0, the p660-6M1 provides the power, capacity, and expandability needed for mission-critical applications.

The Model 6M1 provides excellent midrange performance for transaction processing (TPC-C), Web serving (Specweb99), and server-side Java application processing (Specjb29). The p660-6M1 derives its power from two, four, six, or eight RS64 IV 750 MHz processors with 8 MB of L2 cache. For entry-level configurations, two or four RS64 III 500 MHz processors with 4 MB of L2 cache are available.

Memory on all p660 servers uses IBM's Chipkill technology, which corrects double bit-errors, and in the event of a high error rate, the offending section of memory off-line and logs a service action message for the system administrator to schedule when convenient.

### IBM @serverSeries—An Overview 

The drawers consist of a 5 CEC drawer (Figure 1.15) with processors, memory, and the surrounding system logic, plus one or two I/O drawers, also 5U high. Primary I/O drawer (Figure 1.16) is required, so a base system is 10U (17.5 inches) high.

| Feature | Description |
| :--- | :--- |
| Processor Type | RS64 IV, RS64 III (entry) |
| Memory Capacity | Up to 32 GB |
| Memory Technology | IBM Chipkill |
| I/O Drawers | Primary (5U), Optional Secondary (5U) |
| PCI Slots | 14 hot-plug (4x32-bit, 10x64-bit) |
| Media Bays | 3 (CD-ROM, Diskette, optional Tape drive) |
| Power Options | 220-volt AC or 48V DC |
| Compliance | NEBS Level 3 (for telecom environments) |

- 1-way 600 MHz RS64 IV with 2 MB of L2 cache
- 2- and 4-way 600 MHz RS64 IV with 4 MB of L2 cache per processor
- 1-, 2-, and 4-way 750 MHz RS64 IV with 8 MB of L2 cache per processor
- (Model 6H1 only) 6-way 750 MHz RS64 IV with 8 MB of L2 cache per processor
