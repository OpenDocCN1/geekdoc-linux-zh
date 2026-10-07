+   - Ethernet 10/100 Mbps

+   - Gigabit (10/100/1000 Mbps) Ethernet

+   - Two Ultra3-SCSI ports (internal)

+   - One parallel port

+   - Three serial ports (one serial port is accessible either from the front or the rear)

+   - Two HMCs (Hardware Management Consoles)

+   - Keyboard

+   - Mouse

If the user wishes to run AIX 5L v5.1 or v5.2, then an AIX 5L license and one year of IBM Software Maintenance for AIX (SWMA) is included with the Express Configuration. Users who intend to run the Linux operating system must purchase Linux separately from a Linux distributor. The p615 Linux-ready Express Configurations include a diskette drive for loading diagnostics code for hardware service.

The pSeries 615 system architecture is shown in Figure 1.6. The heart of the system is the Dual Chip Module (DCM) at the upper right of the diagram. It contains the 1.2 GHz POWER4+ processor chip, packed together with the 8 MB L3 cache and main memory control. The 1-way p615 configurations use a processor chip with a single processor core, while the 2-way systems use processor chips with two cores (as depicted).

Although the interface from the memory controller on the DCM is 16 bytes (two 8-byte bidirectional)), the interface to the DDR (Double Data Rate) memory is 32 bytes wide. This is accomplished by buffering in the synchronous memory interface (SMI) chips and fact that the DCM to SMI interface runs at double the clock rate of the SMI memory interface. The point is to be that the cost-effective design of the p615 does not sacrifice L3 cache to memory bandwidth because of a limited number of pins on the DCM. There are eight memory DIMM slots, and memory features come in quads (i.e., four DIMMs). If only four DIMMs are needed for the required memory