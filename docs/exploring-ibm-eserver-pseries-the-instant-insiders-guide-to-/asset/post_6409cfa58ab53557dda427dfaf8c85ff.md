
![](img/29c52a1767a1e621ce6343faa9399737_178_0.png)

**Figure 2.8.** IBM TotalStorage Enterprise Tape System 3590.

ten as a logical volume to an attached TotalStorage Enterprise Tape System 3590, and a copy of the virtual volume remains in cache in the 3494 VTS for fast data access if needed. The 3404-B10 provides four to six tape drives and 648 GB (1,296 GB compressed) of tape volume cache. Model B20 can accommodate six to 12 drives and 2,592 GB (5,184 GB compressed) of tape volume cache. These products are supported on many operating systems, including AIX 5L.

# SCSI I/O Adapters

Small Computer System Interface adapters (called controllers when integrated into the system planar) were introduced in Chapter 1. Figure 2.9 summarizes the SCSI capabilities available for the pSeries. These adapters manage the data flow between the computer system and other devices (e.g., auxiliary storage devices). These controllers are specialized processors that do most of their work independent of the main processor. Most pSeries systems have SCSI capability built into the system planar. Adapters, are installed in a PCI slot inside the computer and attach via cable to the auxiliary storage. The adapter uses one address.

| IBM SCSI Adapter | Feature Code | Bus Type(s) | Maximum Data Rate (MB/sec) | RAID Support | Connection |
|---|---|---|---|---|---|
| Dual Channel Ultra3 SCSI | 6203 | LVD & SE | 160 | N | Internal & External |
| Universal Differential Ultra SCSI | 6204 | Diff. | 40 | N | External |
| Single-Ended Ultra SCSI | 6206 | SE | 40 | N | External |
| 4-Channel Ultra3 SCSI RAID | 2498 | LVD | 160 | Y | Internal & External |

**Figure 2.9.** SCSI adapter summary.

# SCSI Adapter Cards

The following adapters are available for pSeries servers to attach the SCSI devices discussed earlier in this chapter. There are many older PCI SCSI adapters that may be supported but are no longer available. However, latest adapters can support all types of SCSI devices. The SCSI bus protocol functions so if an adapter is capable of Ultra3-SCSI speed (160 Mbps), it can still support older, lower speed devices. However, if a lower speed device is attached on the bus, the performance of all devices attached to that bus cannot be any faster than the slowest device. There are available for pSeries servers a variety of cable options to allow attaching SE and differential devices to these adapters.

# Dual-Channel Ultra3 SCSI Adapter (#6203)

This adapter provides two Ultra3 SCSI (160 Mbps) buses, each of which can be internal or external. It occupies one 64-bit PCI slot, and being a 64-bit adapter, provides excellent throughput for high-performance applications. The adapter negotiates with each device on channel to run at its maximum speed. External devices default to 20 Mbps (to ensure signal quality), but can be Ultra3 SCSI if the external device supports that rate. The two SCSI buses are independent, so they could run at different speeds depending on the attached devices. To fully utilize the power of this adapter, devices must support Ultra3 SCSI LVD attachment. For all SCSI installations, cabling limitations may reduce the number of possible devices below the supported maximum of 15. The adapter conforms to Ultra3 SCSI documentation and uses a mini-68-pin High Density Cable Interconnect (HDCI).

# Universal Differential Ultra SCSI Adapter (#6204)

This adapter provides one SCSI-2 (20 Mbps) or Ultra3 SCSI (40 Mbps) bus that supports both internal and external devices. It occupies one 32-bit PCI slot. It is a “universal” adapter, which means that it can operate in 3.3-volt or 5.0-volt PCI slots. This capability allows it to be used in all pSeries servers—including the newer ones which have 3.3-volt PCI slots, and the older ones which offer 5.0-volt PCI slots. The adapter negotiates with each device on the bus to run at either 20 Mbps or 40 Mbps. External devices default to 20 Mbps (to ensure signal quality) but can be operated at Ultra3 SCSI if the external device supports those speeds. Cabling limitations may reduce the number of possible devices below the supported maximum of 15. The adapter conforms to SCSI-2 and Ultra3 SCSI documentation (X392/048), and uses a shielded 68-pin connector.

# PCI Single-Ended Ultra SCSI Adapter (#6206)

This PCI Single-Ended Ultra SCSI Adapter is a good solution for large block data transfers (greater than 64K bytes) to multiple disks, since it can transfer data at rates up to 40 Mbps. It supports 15 internal and 15 external devices. However, if single-ended devices are attached to the external part of this adapter, both ports will automatically be at 20 Mbps to preserve signal quality on the external bus. The adapter conforms to SCSI-2 and Ultra3 SCSI documentation (X392/048), and uses a shielded 68-pin connector.

# PCI 4-Channel Ultra3 SCSI RAID Adapter (#2498)

The PCI 4-Channel Ultra3 SCSI RAID Adapter (#2498) is a non-bootable high-performance Ultra3 SCSI RAID adapter providing RAID 0 (data striping), 1 (mirroring), and 5 (striping with parity protection) capabilities that can address up to 60 Ultra3 SCSI disk drives on two internal and four external independent Ultra3 SCSI buses. Two of the external ports are shared with the internal parts, so ports may be used for internal attachment or for external attachment, but not for both. If this adapter is attached to the internal backplane of the pSeries server, its performance will be limited by the maximum speed supported on that backplane.

To increase the data writing performance, a 128 MB fast-write cache that utilizes nonvolatile RAM is provided as a standard, resident part of the adapter. During the unlikely event of a PCI 4-Channel Ultra3 SCSI RAID failure, a replacement adapter can be installed and the fast-write cache can be removed from the failing adapter and installed in the new adapter to maintain data integrity. The 128 MB fast-write cache can provide a significant improvement in data throughput and response time during certain write operations compared to adapters without a fast-write cache.

# Integrated SCSI Controllers

Small Computer System Interface (SCSI) controllers are integrated onto the planars of all currently available pSeries and RS/6000 systems. Since these controllers do not consume an adapter slot, they provide significant value in terms of both function and PCI slot utilization. Based generally on the time at which the pSeries system was announced, both the number of integrated controllers and their SCSI function will vary.

For example, the new SCSI 615 Models 6C and 6E3 offer dual Ultra3 SCSI controllers for attaching internal devices. The older pSeries 660 Model 6M1 offers one Ultra3 SCSI controller for internal devices (runs at SCSI-2 full speed of 20 Mbps due to internal backplane limitations) and one Ultra-2 SCSI external controller (80 Mbps). And the still RS/6000 Model 150 offers only one Ultra3 SCSI controller (40 Mbps) for attaching internal devices. This significant level of SCSI attachment capability integrated into the base system electronics, like the increases in processor power and memory density, is another example of the impact of the rapid advances in large-scale integration of logic circuitry on the value of pSeries servers.

# SSA Adapters

Unlike SCSI adapters, there have been several earlier Serial System Architecture (SSA) adapters for RS/6000 and pSeries servers, some of which are supported on current pSeries models. However, the only available adapter for attaching SCSI drives to pSeries servers is the Advanced SerialRAID Plus SSA Adapter (#6230), which offers the most current level of SSA attachment capability.

# Advanced SerialRAID Plus SSA Adapter (#6230)

This RAID adapter supports up to two loops of 48 devices (a total of 96 disks, with an instantaneous data transfer rate of 160 Mbps per loop). The adapter can be configured for several modes.

In 8-way or eight-initiator-RAID mode, up to eight adapters can operate on the same loops of disks, allowing multiple server hosts to share loops of disks. The adapter allows 2-way or two-initiator RAID 1 (mirroring), RAID 0+1 (striping with mirroring), and RAID 5 (striping with distributed parity) modes, as well as single-initiator RAID 0 operation. This adapter provides the necessary functionality for shared data access and high-availability configurations. The adapter supports hot spares in RAID 5 and RAID 0+1 configurations, as well as system boot from a non-RAID SSA disk.
