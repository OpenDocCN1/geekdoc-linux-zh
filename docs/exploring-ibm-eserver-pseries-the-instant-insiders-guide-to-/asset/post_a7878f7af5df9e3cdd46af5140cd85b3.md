
## Options and Peripherals 143

![](img/29c52a1767a1e621ce6343faa9399737_169_0.png)

**Figure 2.7.** The IBM 2105 Enterprise, also known as “Shark.”

Toler design features include redundant power, cooling, adapters, buses, and processor complexes. Using IBM TotalStorage Expert, a network-enabled integrated storage management tool, systems administrators can analyze and manage ESS storage and related tape library resources among the attached servers as requirements change. This Web-based software allows users to monitor and manage the ESS from anywhere in the world using company-secured network and intranet connections.

## Optical Disk Storage

Optical drives use laser beams and reflective disks to record and read information. Two general types of optical disk storage are used with pSeries systems: internal devices as CD-ROM drives and optical libraries, which are used in applications to eliminate storage of massive amounts of paper or microfiche records. CD-ROM drives use the same technique to read information as audio compact discs do and can be used for many different information distribution applications. They are limited to reading information prestored on the CD-ROM disk and cannot change that information. Rewritable optical disk drives can read and write information on optical disks.

## Internal Optical Drives

The internal CD-ROM, DVD-ROM, and DVD-RAM drives are designed to be installed inside the pSeries system in half-high 5.25-inch media bays. On many pSeries models, a CD-ROM drive is standard. For the p650, either CD-ROM or DVD-ROM may be selected, while on the p615 all devices are optional. CD-ROM disks store 650 MB of information and attach to a SCSI I/O controller inside the pSeries drive. An audio jack is provided on the bezel of the CD-ROM drive. The 48x (max) CD-ROM (#2633) provides a data transfer rate of 7,200 KBPS, but older systems have slower CD-ROM models, such as 16x (2,400 KBPS) or 32x (4,800 KBPS).

Most pSeries servers offer the 16x/48x IDE DVD-ROM drive (#2634). On the p650, the 16x/48x SCSI DVD-ROM drive (#2635) with the same specifications is offered. This device can read 650 MB CD-ROM disks at 7,200 KBPS, as well as 4.7 GB and double-sided 9.4 GB DVD-RAM disks at rates of over 22 Mbps. It can also read Type II RAM disks. Although this very versatile device is compatible with most disks, it does not support DVD video. The new p615 uses 8x/24x IDE Slimline DVD-ROM drive (#2640) with the same compatibility characteristics, which has a slightly slower interface.

Also available on pSeries servers is an internal DVD-RAM drive (#2663). This is a multifunction device capable of reading and writing 4.7 GB and 9.4 GB DVD-RAM disks and of reading both CD-ROM and CD-recordable disks. It is a 1x DVD write device (1,350 KBPS) and a 2x DVD read device (2,705 KBPS). It provides 24x performance (3,600 KBPS) as a CD-ROM device. The DVD-RAM goes in a media bay of the pSeries system is attached to a SCSI-2-capable port. The DVD-RAM drive may be used for boot/install from CD-ROM disks and for backup/restore using DVD-RAM disks. In past, tape devices were the only media option for backup and restore. The DVD-RAM provides the ability to boot/install and to backup/restore using a single media device.

## 7210 External DVD-RAM Drive

The 7210 Model 025 External DVD-RAM Drive is a self-contained package designed to sit beside a pSeries system. It provides an externally attachable method (SCSI-2) of adding DVD-RAM capability to pSeries systems. Its characteristics are generally the same as those listed above the internal DVD-RAM device. This external device is likely to be useful on older RS/6000 systems, which do not offer the internal DVD-RAM option available on pSeries servers.

## 3995 Optical Library Dataservers

The 3995 Optical Library Dataservers are rewritable optical libraries that attach directly to pSeries systems, providing on-line access to vast amounts of information at a lower cost than magnetic disks.

Documents, forms, and records currently in paper form can be scanned into an electronic format and stored in an optical library such as the 3995, along with data traditionally stored on microfiche or microfilm. This on-line data can be retrieved, displayed, and printed, and it can be stored on optical disk cartridges for long-term (500 years for WORM). Multiple users can access the data simultaneously, and optical storage is the intermediary medium between disk and tape in hierarchical storage management applications.

Various models of 3995 Optical Library Dataservers offer a range of performance and capacity. The multifunction optical drives used in the 3995 can concurrently support a number of optical disk formats (Permanent Write-Once-Read-Many [WORM], Continuous Possible WORM, and rewritable cartridges) and capacities. The unformatted data storage capacity of Model C6 provides a data transfer rate of 7,200 KBPS, but older systems have slower CD-ROM models, such as 16x (2,400 KBPS) or 32x (4,800 KBPS).

## Tape Storage

Most pSeries servers offer the 16x/48x IDE DVD-ROM drive (#2634). On the p650, the 16x/48x SCSI DVD-ROM drive (#2635) with the same specifications is offered. This device can read 650 MB CD-ROM disks at 7,200 KBPS, as well as 4.7 GB and double-sided 9.4 GB DVD-RAM disks at rates of over 22 Mbps. It can also read Type II RAM disks. Although this very versatile device is compatible with most disks, it does not support DVD video. The new p615 uses 8x/24x IDE Slimline DVD-ROM drive (#2640) with the same compatibility characteristics, which has a slightly slower interface.

## Tape Options

For smaller systems, external tape drives are often the easiest way to back up or install the system. For larger systems with hundreds of gigabytes of data, a single tape drive is simply not sufficient either in capacity or speed to fill the bill. For these systems, larger tape libraries that can automatically load many tape cartridges into multiple tape drives provide an excellent solution.

## 4-mm Tape Options

The 4-mm digital audio tape (DAT) employs an advanced helical scan recording technology. In helical scanning, tape passes over the tape drive's recording head at an angle, creating thousands of packed tracks. The 4-mm technology fills the gap between 8-mm and 3-inch tape.

## 7206 External 4-mm Tape Drive Model 220

The 7206 4-mm Tape Drive is an external device that can be used with all pSeries models. It is a self-contained device designed to rest beside a system. It is attached to the pSeries via a cable to a port and gets its power from a standard electrical socket. The 7206-220 is primarily used for disk backup, data archiving, and information distribution. It provides 20 GB cartridge capacity, expandable to a compressed capacity to 40 GB using DDS-4 and either Ultra-SCSI or low-voltage differential (LVD) interfaces.

## 7206 External Tape Drive Model VX2

The 7206-VX2 is an external tape drive offering the emerging VXA tape technology mentioned above for the internal tape drive (#6120). It uses VXA tape cartridges and offers 80 GB native and 160 GB capacity.
