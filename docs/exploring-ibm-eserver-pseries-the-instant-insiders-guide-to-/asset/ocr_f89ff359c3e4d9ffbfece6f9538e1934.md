# IBM server pSeries—An Overview 53

from the processor complex (DEC drawer) to the I/O drawer is composed of two RIO (remote I/O) ports (see Figures 1.8a and 1.8b), connected in a loop. Each RIO port has an aggregate bandwidth of 1 Gbps (500 MBps bidirectional). With one I/O drawer, the overall bandwidth is 1 Gbps (just as for the p620 models), but with two I/O drawers, transmissions to each drawer are sent from the CEC by the path to each drawer and the overall bandwidth is doubled, to 2 Gbps. In the event of a failure in one of the RIO ports, all traffic is routed on the working port. Although the bandwidth falls back to 1 Gbps, the system continues to run.

The primary I/O drawer features two integrated SCSI controllers (SCSI-2 F/W [fast/wide] internal and Ultra2-SCSI external), an Ethernet 100 controller, four slots and one parallel path, keyboard and mouse ports. In addition, the I/O drawer includes 14 hot-plug PCI slots (four 32-bit and ten 64-bit), which allow for addition or removal of adapter cards when the system is running, and three media bays. Two of the media bays are filled by default with a CD-ROM drive and a diskette drive. The third is available and is used most for a tape drive. With the CEC, a redundancy option is available for the hotplugplug supplies and cooling fans in the I/O drawer. This I/O drawer is also used on the pSeries 660 660M1.

Since the I/O drawers do not provide disk bays

The pSeries 660 Models 6H1 and 6H0 are powered by 220-volt AC power, or alternatively, for the special needs of the telecommunications industry, by 48 volts DC. Also, for telecommunications central office or other environments with harsh operating conditions, these systems are designed for NEBS Level 3 compliance.

With their highly reliable and scalable design and performance (roughly twice that of the pSeries 640), the p660-6H1 and p660-6H0