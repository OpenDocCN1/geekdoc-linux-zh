154 Exploring IBM @serverPSeries

# Dual-Channel Ultra3-SCSI Adapter (#6203)

This adapter provides two Ultra3-SCSI (160 Mbps) buses, each of which can be internal or external. It occupies one 64-bit PCI bus slot, and being a 64-bit adapter, provides excellent throughput for high-performance applications. The adapter negotiates with each device on each channel to run at its maximum speed. External devices default to 20 Mbps (to ensure signal quality), but can be Ultra3-SCSI speed if the external device supports that rate. The two SCSI buses are independent, so they could run at different speeds, depending on the attached devices. To fully utilize the power of this adapter, devices must support Ultra3-SCSI LVD attachment. For all SCSI installations, cabling limitations may reduce the number of possible devices below the supported maximum of 15. The adapter conforms to Ultra3-SCSI documentation and uses a mini-68-pin Very High Density Cable Interconnect (VHDCI) connector.

# Universal Differential Ultra-SCSI Adapter (#6204)

This adapter provides one SCSI-2 (20 Mbps) or Fast-20 Ultra (40 Mbps) bus that supports both internal and external devices. It occupies one 32-bit PCI bus slot. It is a “universal” PCI adapter, which means that it can operate in 3.3-volt or 5.0-volt PCI slots. This capability allows it to be used in all pSeries servers—including the newer ones, which have only 3.3-volt PCI slots, and the older ones, which offer 5.0-volt PCI slots. The adapter negotiates with each device on the bus to run at either 20 Mbps or 40 Mbps. External devices default to 20 Mbps (to ensure signal quality) but can be operated at Fast-20 Ultra if the external device supports those speeds. Cabling limitations may reduce the number of possible devices below the supported maximum of 15. The adapter conforms to SCSI-2 and Fast-20 Ultra documentation (X3T92/90-048), and uses a shielded 68-pin connector.

# PCI Single-Ended Ultra-SCSI Adapter (#6206)

This PCI Single-Ended-Ultra-SCSI Adapter is a good solution for large block data transfers (greater than 64K bytes) to multiple disks, since it can transfer data at rates up to 40 Mbps. It supports 15 internal devices