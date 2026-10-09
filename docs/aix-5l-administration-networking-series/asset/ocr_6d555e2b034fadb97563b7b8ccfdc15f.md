| Device State | State Definition |
| --- | --- |
| Defined | Device defined but not available for use |
| Stopped | Device configured but not available |
| Available | Device configured and available |

Table 9-8. Device States

# SMALL COMPUTER SYSTEM INTERFACE

The most common device interface for the pSeries and RISC System /6000 is the small computer system interface (SCSI). The SCSI standard defines a generic interface and command protocol that will support most device types. Devices are attached in a daisy-chain fashion to the host adapter. The total chain length cannot exceed the distance maximum for the adapter type.

# SCSI-1 and SCSI-2

The RISC System /6000 supports both SCSI-1 and SCSI-2 adapters and devices. Both SCSI-1 and SCSI-2 devices may be mixed on either adapter type; however, throughput to the device will be limited to SCSI-1 speeds. The **cfmgr** queries the device type during SCSI device configuration and records the SCSI type. This eliminates the need for device drivers to continually query the SCSI type to determine whether extended SCSI-2 commands are supported. SCSI-1 support provides transfer rates up to 4 megabytes per second. The SCSI-2 Fast SCSI mode extends synchronous transfer rates to 10 megabytes per second. SCSI-2 signal control is also two to three times faster than SCSI-1. A maximum of 8 devices can be on a single SCSI-1 or SCSI-2 bus.

# Single-Ended and Differential SCSI

Single-ended SCSI connections have a combined distance limitation of 6 meters. The logic level of each wire is based on the voltage difference with a common ground. Differential SCSI connections can run up to 25 meters. Logic levels on differential connections are based on the potential difference between two signal wires.

Single-ended connections can be a real problem with some RS /6000-9XX systems. The SCSI cable management arms in early 9XX racks eat up approximately 4.75 meters of the total 6-meter cable length. A single-ended SCSI to a differential SCSI adapter can be used to get around the problem.

# Fast SCSI

The SCSI Fast-20 supports up to 8 devices but only a cable length of 3 meters for single-ended. Fast differential SCSI can reach a cable length of 25 meters with a maximum bus speed of 20MB/Sec.