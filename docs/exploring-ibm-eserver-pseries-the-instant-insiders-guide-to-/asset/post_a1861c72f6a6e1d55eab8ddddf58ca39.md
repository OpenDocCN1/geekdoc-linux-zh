
![](img/29c52a1767a1e621ce6343faa9399737_43_0.png)

**Figure 1.3.** pSeries 610 Models 6E1 and 6C1.

- CD-ROM drive
- 1.44 MB 3.5-inch diskette drive
- Built-in service processor
- Integrated I/O ports (do not require use of PCI slots)
- Two 10/100 Mbps megabits per second) Ethernet
- Two Ultra3-SCSI ports (internal and external)
- One parallel port
- Three serial ports (on the rack model p610-6C1, one serial port is accessible either from the front or the rear)
- Keyboard
- Mouse

# Exploring IBM @serverSeries

Processor speed or clock rate is just one factor in determining system-level performance, and the pSeries 610 design provides outstanding internal bandwidth to both memory and I/O devices for a system in this price class. As shown in Figure 1.4, the processor-to-memory bus is 128 bits wide, plus 8 ECC bits, which yields a maximum bandwidth of 1.44 Gbps (gigabytes per second) with double-bit error detection and single-bit error correction. The I/O bus can operate up to 528 Mbps with parity checking. This speed and internal error checking features provide high-system performance in an entry-level UNIX server.

The p610 is expandable above either adding a second 333 MHz processor or one or two of the 375 MHz processors with 4 MB of Level 2 (L2) cache or the powerful 450 MHz processors with 8 MB of L2 cache each. Memory can be added up to 8 GB in memory DIMMs (Dual In-line Memory Modules). Disk storage begins with a single 18.2 GB drive mounted on one of the internal bays and can grow to a 291.2 GB (more than a quarter of a terabyte) using 36.4 GB drives. In addition to the significant number of I/O interfaces integrated into the system planar (see base configuration detailed earlier), there are five PCI slots, three of which are 64-bit capable.

An interesting characteristic of the pSeries 610 is the breadth of reliability, availability, and serviceability (RAS) features offered in an entry-priced system. These features may especially important for small companies, who have limited information technology skills and resources to deal with system problems, and for retail stores or branch offices systems scattered in remote locations where no computer specialist is available. The p610-61C and the p610-61E are the first pSeries to offer Light Path Diagnostics. With Light Path Diagnostics, if a component fails, a first-mounted attention light is turned on. The user looks at the system indicator LED (Emitting-Device) array to see which component is having a problem; this array is similar to those found on many office copiers to help locate paper jams. Finally, there are additional LEDs located near each component. Light Path Diagnostics makes it easy to locate the component to be replaced; it is particularly helpful if a technician is not on site and is working by telephone with local personnel to correct a problem.

The service processor, provided as a standard component on the p610 and all other pSeries servers, enables RAS functions such as monitoring of power and temperature parameters, error log analysis and

# IBM @server pSeries—An Overview 19

| 4 MB L2 / w/ 333 MHz | 4 MB L2 / w/ 375 MHz | 8 MB L2 / w/ 450 MHz |
| :--- | :--- | :--- |
| Processor Card 166.5 MHz / w/ 333 MHz | POWER3-II 250 MHz / w/ 375 MHz, 333 MHz, or 375 MHz | 225 MHz / w/ 375 MHz, or 450 MHz |

| 4 MB L2 / w/ 333 MHz | 4 MB L2 / w/ 375 MHz | 8 MB L2 / w/ 450 MHz |
| :--- | :--- | :--- |
| Processor Card 166.5 MHz / w/ 333 MHz | POWER3-II 250 MHz / w/ 375 MHz, 333 MHz, or 375 MHz | 225 MHz / w/ 375 MHz, or 450 MHz |

| 4 MB L2 / w/ 333 MHz | 4 MB L2 / w/ 375 MHz | 8 MB L2 / w/ 450 MHz |
| :--- | :--- | :--- |
| Processor Card 166.5 MHz / w/ 333 MHz | POWER3-II 250 MHz / w/ 375 MHz, 333 MHz, or 375 MHz | 225 MHz / w/ 375 MHz, or 450 MHz |

| PCI Bridge | PCI Bridge |
| :--- | :--- |
| 1 PCI Slot 64 bit 33 MHz 5v | 2 PCI Slots 64 bit 50 MHz 3.3v |
| 2 PCI Slots 32 bit 33 MHz 5v | |

| Data | 6xx MX Bus 66 MHz |
| :--- | :--- |
| PCI Bridge | |

| 4 MB L2 / w/ 333 MHz | 4 MB L2 / w/ 375 MHz | 8 MB L2 / w/ 450 MHz |
| :--- | :--- | :--- |
| Processor Card 166.5 MHz / w/ 333 MHz | POWER3-II 250 MHz / w/ 375 MHz, 333 MHz, or 375 MHz | 225 MHz / w/ 375 MHz, or 450 MHz |

| Data Bus | 16 Bytes @ 91.4 MHz / w/ 333 MHz | 16 Bytes @ 93.7 MHz / w/ 375 MHz | 16 Bytes @ 91.4 MHz / w/ 333 MHz | 16 Bytes @ 93.7 MHz / w/ 375 MHz | 16 Bytes @ 90.0 MHz / w/ 450 MHz |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 6xx Address Bus | | | | | | |
| 6xx Data Bus | | | | | | |

| SCSI Controller | External Ultra-SCSI |
| :--- | :--- |
| SCSI Controller | Internal Ultra-SCSI |

| Memory 512 MB - 8 GB | POWER3-II 250 MHz / w/ 375 MHz, 333 MHz, or 375 MHz | 225 MHz / w/ 375 MHz, or 450 MHz |
| :--- | :--- | :--- |
| Memory Address | Addr/Cntl |

| Integrated Service Processor | ISA Bridge | 10/100 Ethernet | 10/100 CD ROM | Super port I/O |
| :--- | :--- | :--- | :--- | :--- |
| System Planar | | | 3rd serial | |

Figure 1.4. pSeries 610 Models 6CI and 6EI system design.

# Exploring IBM server pSeries

alerts, auto dial-out in the event of predicted or actual failures, and automatic reboot after a variety of failures.

The p610 has six hot-swappable front-accessible disk drive bays, which allow disks to be replaced while the system is running. If the optional redundant power supply is installed, the system will not go down if one supply fails, and the hot-plug fans allow the system to keep running. Similarly, if one fan fails, the p610 has a built-in processor that can call home in the event of failures.

The p610 has 1.2 GHz POWER4+ pSeries 615 Specifics

The p615 is the most recent pSeries with features.

The pSeries 615 system architecture is shown in Figure 1.6. The heart of the system is the Dual Chip Module (DCM) at the upper right of the diagram. It contains the 1.2 GHz POWER4+ processor chip, packed together with the 8 MB L3 cache and main memory control. The 1-way p615 configurations use a processor chip with a single processor core, while the 2-way systems use processor chips with two cores (as depicted).

Although the interface from the memory controller on the DCM is 16 bytes (two 8-byte bidirectional)), the interface to the DDR (Double Data Rate) memory is 32 bytes wide. This is accomplished by buffering in the synchronous memory interface (SMI) chips and fact that the DCM to SMI interface runs at double the clock rate of the SMI memory interface. The point is to be that the cost-effective design of the p615 does not sacrifice L3 cache to memory bandwidth because of a limited number of pins on the DCM. There are eight memory DIMM slots, and memory features come in quads (i.e., four DIMMs). If only four DIMMs are needed for the required memory

# IBM @server pSeries—An Overview 21

![](img/29c52a1767a1e621ce6343faa9399737_47_0.png)

**Figure 1.5.** pSeries 610 Models 6CI and 6EI system design.

The smallest p615 includes the following hardware:

- 1.2 GHz POWER4+ processor
- 8 MB L3 cache
- 1 GB of SDRAM with ECC
- Four hot-swappable disk bays
- Slim-line DVD-ROM drive
- Slim-line diskette drive
- Built-in service processor
- Integrated I/O ports (do not require use of PCI slots)
- 10/100 Mbps Ethernet
- Gigabit (100/1000 Mbps) Ethernet
- Two Ultra3-SCSI ports (internal)
- One parallel port
- Three serial ports (one serial port is accessible either from the front or the rear)
- Two HMCs (Hardware Consoles)
- Keyboard
- Mouse

If the user wishes to run AIX 5L v5.1 or v.2, then an AIX 5L license and one year of Software Maintenance for AIX (SWMA) is included with the Express Configuration. Users who intend to run the Linux operating system must purchase Linux separately from a distributor. The p615 Linux-ready Express Configurations include a diskette drive for loading diagnostics code.

The pSeries615 system architecture is shown in Figure 1.6. The heart of the system is the Dual Chip Module (DCM) at the upper right of the diagram. It contains the 1.2 GHz POWER4+ processor chip, packed together with the 8 MB L3 cache and main memory control. The 1-way p615 configurations use a processor chip with a single processor core, while the 2-way systems use processor chips with two cores (as depicted).

Although the interface from the memory controller on the DCM is 16 bytes (two 8-byte bidirectional)), the interface to the DDR (Double Data Rate) memory is 32 bytes wide. This is accomplished by buffering in the synchronous memory interface (SMI) chips and fact that the DCM to SMI interface runs at double the clock rate of the SMI memory interface. The point is to be that the cost-effective design of the p615 does not sacrifice L3 cache to memory bandwidth because of a limited number of pins on the DCM. There are eight memory DIMM slots, and memory features come in quads (i.e., four DIMMs). If only four DIMMs are needed for the required memory
