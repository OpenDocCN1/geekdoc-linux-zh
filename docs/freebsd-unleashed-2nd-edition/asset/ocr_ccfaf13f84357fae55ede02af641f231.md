# TABLE 18.4 Continued

| Standard | Transfer Mode | Transfer Speed | Max Cable Length | Devices/IDs | Connector |
| :--- | :--- | :--- | :--- | :--- | :--- |
| SCSI-3 | Ultra SCSI | 20 MBps | 1.5–3m | 4–8 | 50-pin |
| | Wide Ultra SCSI | 40 MBps | 1.5–3m | 4–16 | 68-pin |
| | Ultra2 SCSI | 40 MBps | 12m | 8 | 50-pin |
| | Wide Ultra2 SCSI | 80 MBps | 12m | 16 | 68-pin |
| | Ultra3 SCSI | 160 MBps | 12m | 16 | 68-pin |
| | Ultra160 SCSI | 160 MBps | 12m | 16 | 68-pin |
| | Ultra320 SCSI | 320 MBps | 12m | 16 | 68-pin |

For all its "can you top this?" naming conventions, however, SCSI is relatively well behaved and predictable when it comes to its capabilities. Each successive standard is twice as fast as the previous, and although there's a truly astonishing number of different cable styles made for SCSI devices, the connector standard has remained mercifully steady over the years. This means that for the most part, any modern SCSI controller will recognize—and properly handle—any SCSI device that was built to an earlier standard.

An SCSI device chain can handle up to the number of devices specified by the standard, usually 8 or 16. That's a far cry from the strictly regimented four (primary and secondary, master and slave) of the IDE/ATA structure. What's more, the order of these devices doesn't matter; there are no such things as "masters" or "slaves" in SCSI to dictate cabling order. There's only the controller, or host adapter (which takes up one of the device IDs), and the rest of the devices.

SCSI also has clear advantages if you're using external disks. IDE/ATA provides no good way to hook an external disk to the internal bus; sometimes you can get away with using the parallel (printer) port, as with Iomega Zip drives, but this is an astonishingly slow interface and is unusable for any general purpose. SCSI is the only game in town for external disks until FireWire (IEEE 1394) becomes prevalent.

The biggest problem with SCSI is, simply, price. SCSI disks are generally pricier than similar-sized IDE disks by 50 to 100 percent. Beyond that, there's the cost of the host adapter card, which you have to buy separately from the motherboard. (Very few motherboards today are made with built-in SCSI cards, although the number is, in fact, rising.) These controllers aren't cheap.

If you're interested in going the SCSI route, you should know that there are more pitfalls to avoid that are beyond the scope of coverage here. These include terminators, the SCSI BIOS, setting device IDs (with jumpers), and what happens when you mix "narrow" and "wide" devices on the same chain. Further reference can be found in the many books dedicated to the subject or at the PC Guide Web site (http://www.pcguide.com).