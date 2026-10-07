
## 122 Exploring IBM@serverSeries

hand-held computers, audio system, television sets, there have been rapid advances in circuit integration and electronic packaging technologies. The use of Very Large Scale Integration (VLSI) and double-Surface Mount Technology (SMT) has reduced the overall size of the systems. VLSI is an electronic fabrication technology that allows literally thousands of electronic circuits to be packaged on a single chip. The type of VLSI circuitry used in pSeries computers is less than 3-micron CMOS (CMOS stands for Complementary Metal Oxide Semiconductor, which is a type of VLSI circuitry.) CMOS is fairly high-speed circuitry with low power requirements, which reduces system power supply and cooling requirements. The advances in circuit density for both logic and memory chips have been supported by innovations in circuit packaging and connector technologies. Another significant factor has been the reduction in size (and increase in capacity) of storage devices as disk drives, diskettes, and tape drives.

Several types of mechanical enclosures are used to house the various elements of pSeries systems. There are floor-standing enclosures, desksides, that allow for a bit of expansion in main memory, disk storage, I/O adapters, and peripheral devices, which can be positioned beside a desk in an office environment. Many pSeries systems use another enclosure that complies with industry standards. This structure is a 19-inch rack that can house various drawers, such as the CEC drawer with the system electronics, the I/O drawers with PCI slots and disk drives, and drawers for other attached devices. Multiple drawers are installed in one or more racks to build a complete system. Rack heights are measured in EIA units, which amount to 1.75 inches each. Currently available racks are the Model T00 (36 EIA units) and the Model T42 (42 units). The p655, p670, and p690 systems are designed for 24-inch-wide racks to accommodate the expandability of those servers in a single frame.

All pSeries systems are now available only black, using contemporary industrial design. Availability of features in the traditional off-white color is being phased out. The reasons for this change are to eliminate the cost of releasing the very same functional item in two colors and to reduce inventory costs by maintaining stocks of only one part.

## 2 Options and Peripherals

IBM eServer pSeries systems can be found in diverse environments ranging from research laboratories to retail stores to insurance companies. The activities these various users perform vary widely, and so do their computing needs. pSeries systems can be customized to many environments by selecting the appropriate optional equipment. This chapter describes many adapters and peripheral devices that are commonly used with pSeries systems.

Adapters, or feature cards, are circuit boards that are installed in the PCI or PCI-X I/O slots of pSeries systems to provide some additional capacity or function for the system. These feature cards include storage adapters, LAN adapters, graphics accelerators, and cryptographic coprocessors.

Peripherals are devices that are installed in or attach to pSeries systems to perform some specialized function. Disk drives, tape drives, printers, and plotters fall into this category.

It is helpful to understand IBM terminology for these options. Peripheral devices have specific product numbers associated with them (e.g., the 2104-DU3 Expandable Storage subsystem or the 4247 Serial Matrix Printer). Optional features installed in pSeries systems are identified by feature numbers (e.g., the Dual-channel Ultra3-SCSI Adapter is feature #6203, and the pSeries 615 1 GB Memory Expansion feature is #4446. Either product numbers or feature numbers are provided for many of the options covered in this chapter.

### Memory Expansion Options

Nothing seems to grow faster than the computer user's appetite for main memory. Several different options allow the user to expand the main memory in pSeries computers. However, owing to technical differences inside the systems, memory expansion options are not interchangeable among all pSeries models. Main memory systems of all available pSeries and RS/6000 systems use the Error Checking and Correction (ECC) method to detect and offset correct memory problems, as discussed in Chapter 1. The latest POWER4+ servers—p615, p630, p650, p655, p670, and p690—also implement Chipkill memory, decreasing even further the likelihood of a system outage due to memory failure.

The following discussion of memory features covers the currently available pSeries and RS/6000 systems.

### RS/6000 Models 150 and B50 Memory Expansion

The Models 150 and B50 will accommodate up to four ECC 10-ns SDRAM DIMMs. The minimum memory configuration is 128 MB, and the default for this is a single 128 MB DIMM. The DIMMs are available in three sizes: 64 MB (#4149), available only on Model 150, 128 MB (#4150), and 256 MB (#4169). It is not necessary to install these DIMMs in pairs. The maximum memory of 1,024 MB (1 GB) can be achieved with four of the 256 MB DIMMs (#4169).

### RS/6000 Model 170 Memory Expansion

The Model 170 will accommodate up to four ECC 10-ns 200-pin SDRAM DIMMs, which must be installed in pairs. The minimum memory configuration is 256 MB, consisting of two 128 MB DIMMs. The DIMM pairs are available in three sizes: 256 MB (2 × 128 MB) (#4110), 512 MB (#4120), and 1,024 MB (#4121). The maximum memory is 2 GB, which is achieved with the installation of two of feature #4121 (four DIMMs).

### pSeries 610 Models 6C1 and 6E1 Memory Expansion

The p610-6C1 and p610-6E1 use 200-pin 10-ns SDRAM DIMMs, which must be installed in pairs. There is one 16-position (8 DIMM pairs) memory card. The minimum memory configuration is 512 MB, consisting of two 256 MB DIMM pairs are available in two sizes: 512 MB (2 x 256 MB, #4120) and 1,024 MB (2 x 512 MB, #4121). The maximum memory is 8 GB, which is achieved with the installation of eight feature #4121 (16 DIMMs). Note that the p640-B80 and RS/6000 Models 170 and 270.

### pSeries 615 Models 6C3 and 6E3 Memory Expansion

The p615-6C3 and p615-6E3 use 200-pin 10-ns SDRAM DIMMs, which must be installed in pairs. The minimum memory configuration is 1 GB, consisting of four 256 MB DIMMs. The quads are available in four sizes: 1 GB (4 x 256 MB, #4446), 2 GB (4 x 512 MB, #4447), 4 GB (4 x 1,024 MB, #4448), and 8 GB (4 x 2,048 MB, #4449). The maximum memory is 16 GB, which is achieved with the installation of two feature #4449 (eight DIMMs).

### pSeries 630 Models 6C4 and 6E4 Memory Expansion

The p630-6C4 and p630-6E4 use 200-pin 10-ns SDRAM DIMMs, which must be installed in pairs. The minimum memory configuration is 1 GB, consisting of four 256 MB DIMMs. The quads are available in four sizes: 1 GB (4 x 256 MB, #4446), 2 GB (4 x 512 MB, #4447), 4 GB (4 x 1,024 MB, #4448), and 8 GB (4 x 2,048 MB, #4449). The maximum memory is 32 GB, which is achieved with the installation of four feature #4449 (sixteen DIMMs).
