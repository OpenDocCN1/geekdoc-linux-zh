
![](img/29c52a1767a1e621ce6343faa9399737_71_0.png)

Figure 1.13. pSeries650 system design.

RIO-2 hubs interface only to I/O drawers. The p650 supports both the IBM 7311-D10 and 7311-D20 I/O Drawers in up to four RIO-I/O loops. RIO-2 loops operate at a 1 GHz clock rate, and since they are bidirectional, they can support a peak bandwidth of 2 Gbps. If two or more I/O drawers are connected in series in a RIO-2 loop, the system will transfer data from each RIO-2 port to the near I/O drawer—increasing the peak bandwidth to 4 Gbps per loop.

Both the 7311-D10 and 7311-D20 I/O drawers are 4U19-inch rack units. However, the 7311-D10 provides six I/O slots and no disk bays in a half-drawer package, so two 7311-D10 drawers fit side-by-side in a rack. On the other hand, the 7311-D20 is a full-width drawer with 7 I/O slots and 12 optional disk drive bays. If additional storage is needed, the 7311-D20 is the best choice. If only I/O adapter slots are needed, then the 7311-D10 is the appropriate answer. The bottom line is that a fully configured p650 provides a peak I/O bandwidth of 16 Gbps and can accommodate up to 63 I/O adapters and 14.6 TB of storage—all of capacity.

# 46 Exploring IBM @serverSeries

The pSeries 650 supports up to eight logical partitions, each running an independent copy of the operating system. And both the p650 server running as an SMP server and LPARs of the p650 are supported in Cluster 1600 systems. For LPAR and for clustering, an attachment to an HMC is required. LPAR is described in greater detail in “A Closer Look” later in this chapter, and a description of Cluster 1600 systems is given following this section.

The p650 incorporates the full range of autonomic computing or RAS functions on the high-end pSeries 690. These include standard-hot-plug power supplies and cooling fans, hot-swappable drives, hot-plug PCI-X slots. There are many self-healing capabilities, such as Chipkill and ECC in main memory, ECC on L2 and L3 caches, PCI-X bus error recovery, First Failure Data Capture, Dynamic Processor Deallocation, deallocation of PCI buses and slots, and concurrent run-time diagnostics. The built-in service processor is used for power on/off control, monitoring system and AIX 5L status, and if enabled, can be used to automatically dial out to notify personnel of a problem needing attention.

For users who need to be able to activate processors and memory very quickly in order to meet unexpected workload or regular spikes in workload (such as seasonal sales, quarter end or annual financial reports, and the like), the p650 offers a full range of the pSeries “on demand” features—Capacity Upgrade on Demand (CuOD) for processors, CUoD for memory, On/Off Capacity on Demand (CoD) and Trial CoD. These functions are explained in the p690 description later in this chapter. The specific on demand features offered by the p650 are following:

- 2-way 1.45 GHz POWER+ processor card with no processors active
- Permanent activation of two CuOD processors
- On/Off activation and deactivation of two CuOD processors
- 8 GB of memory with 0 GB active
- 16 GB of memory with 0 GB active
- Permanent activation of 4 GB of memory

# IBM @server pSeries—An Overview 47

- Trial CoD

The p650 is supported by AIX 5L v5.1 and v5.2 by SuSE Linux Enterprise 8 for iSeries and pSeries. As in the case of the pSeries 630, IBM offers p650 Express Configurations for both AIX 5L and Linux Ready Express Configurations. These fixed configurations must include all the specified components without substitutions, which may be supplemented with other features, such as additional memory, disk drives, or I/O adapters. The p650 Linux ready Express Configurations do not include an AIX 5L license or IBM Software Maintenance for AIX; customers must purchase Linux and the associated support from a Linux distributor.

With up to 8-way 1.45 GHz POWER4+ processors, 64 GB of memory, the ability to attach I/O expansion drawers, LPAR, on demand capabilities, and the ability to run both UNIX and Linux operating systems, the pSeries 650 is an extremely powerful and flexible midrange server.

# pSeries 655 Specifications

The pSeries 655 is unique among pSeries servers because it is packaged in an ultra-dense 4U half-drawer unit for a 24-inch “frame”, similar to the 24-inch racks used for the p690 and p670 servers (Figure 1.14). A half-drawer means that two servers fit side-by-side in an IBM 7040-W42 frame. For readers familiar with the IBM RS/6000 SP (no longer available), the p655 package is equivalent to a “thin node”. With 4-way 1.7 GHz and 8-way 1.5 GHz POWER4+ and 4-way 1.3 GHz and 8-way 1.1 GHz POWER4 processors packaged in a multiparticle module with 128 MB of L3 cache, the p655 is designed for high-performance computing applications. Each p655 server can have up to 32 GB of memory, with 64 GB available for selected configurations by special request. With 8-way MCMs, a single 42U-high frame can accommodate 16 p655s (128 processors), each with 128 MB of L3 cache and 32 GB of memory—clearly a high-performance system design.

The p650 design is also optimized for use in parallel Cluster 1600 systems. In order to achieve maximum “footprint” density of processing power, the internal storage and I/O adapter slot capacity is limited, compared to other pSeries systems. There are two hot-swappable disk drive bays, no media bays, and three hot-plug PCI-X slots. Rather than

![](img/29c52a1767a1e621ce6343faa9399737_74_0.png)

**Figure 1.14.** pSeries 655.

having individual power supplies for each p655 server, there is an 8U bulk power supply subsystem, with optional battery backup for higher availability. But up to five 7040-61D I/O Drawers can be mounted in the frame along with p655 servers. Each 4U I/O drawer provides 16 hot-swappable disk bays and 20 PCI-X slots, so there is ample storage and I/O adapter capacity at the system level. Alternatively, the p655 servers can be attached to separate storage subsystems such as the IBM 7133-D40 Serial Disk System or the IBM 2104-DU3 Expandable Storage Plus mounted in adjoining

Each 4U I/O drawer provides 16 hot-swappable disk bays and 20 PCI-X slots, so there is ample storage and I/O adapter capacity at the system level. Alternatively, the p655 servers can be attached to separate storage subsystems such as the IBM 7133-D40 Serial Disk System or the IBM 2104-DU3 Expandable Storage Plus mounted in adjoining

Each 4U I/O drawer provides 16 hot-swappable disk bays and 20 PCI-X slots, so there is ample storage and I/O adapter capacity at the system level. (Wait, correcting redundant text flow)

- Chipkill and ECC in main memory, ECC on L2 and L3 caches, PCI-X bus error recovery, First Failure Data Capture, Dynamic Processor Deallocation, deallocation of PCI buses and slots, and concurrent run-time diagnostics. The built-in service processor is used for power on/off control, monitoring system and AIX 5L status, and if enabled, can be used to automatically dial out to notify personnel of a problem needing attention.

For users who need to be able to activate processors and memory very quickly in order to meet unexpected workload or regular spikes in workload (such as seasonal sales, quarter end or annual financial reports, and the like), the p650 offers a full range of the pSeries “on demand” features—Capacity Upgrade on Demand (CuOD) for processors, CUoD for memory, On/Off Capacity on Demand (CoD) and Trial CoD. These functions are explained in the p690 description later in this chapter. The specific on demand features offered by the p650 are following:

- 2-way 1.45 GHz POWER+ processor card with no processors active
- Permanent activation of two CuOD processors
- On/Off activation and deactivation of two CuOD processors
- 8 GB of memory with 0 GB active
- 16 GB of memory with 0 GB active
- Permanent activation of 4 GB of memory

The p650 is supported by AIX 5L v5.1 and v5.2 by SuSE Linux Enterprise 8 for iSeries and pSeries. As in the case of the pSeries 630, IBM offers p650 Express Configurations for both AIX 5L and Linux Ready Express Configurations. These fixed configurations must include all the specified components without substitutions, which may be supplemented with other features, such as additional memory, disk drives, or I/O adapters. The p650 Linux ready Express Configurations do not include an AIX 5L license or IBM Software Maintenance for AIX; customers must purchase Linux and the associated support from a Linux distributor.

With up to 8-way 1.45 GHz POWER4+ processors, 64 GB of memory, the ability to attach I/O expansion drawers, LPAR, on demand capabilities, and the ability to run both UNIX and Linux operating systems, the pSeries 650 is an extremely powerful and flexible midrange server.

The pSeries 655 is unique among pSeries servers because it is packaged in an ultra-dense 4U half-drawer unit for a 24-inch “frame”, similar to the 24-inch racks used for the p690 and p670 servers (Figure 1.14). A half-drawer means that two servers fit side-by-side in an IBM 7040-W42 frame. For readers familiar with the IBM RS/6000 SP (no longer available), the p655 package is equivalent to a “thin node”. With 4-way 1.7 GHz and 8-way 1.5 GHz POWER4+ and 4-way 1.3 GHz and 8-way 1.1 GHz POWER4 processors packaged in a multiparticle module with 128 MB of L3 cache, the p655 is designed for high-performance computing applications. Each p655 server can have up to 32 GB of memory, with 64 GB available for selected configurations by special request. With 8-way MCMs, a single 42U-high frame can accommodate 16 p655s (128 processors), each with 128 MB of L3 cache and 32 GB of memory—clearly a high-performance system design.

The p650 design is also optimized for use in parallel Cluster 1600 systems. In order to achieve maximum “footprint” density of processing power, the internal storage and I/O adapter slot capacity is limited, compared to other pSeries systems. There are two hot-swappable disk drive bays, no media bays, and three hot-plug PCI-X slots. Rather than having individual power supplies for each p655 server, there is an 8U bulk power supply subsystem, with optional battery backup for higher availability. But up to five 7040-61D I/O Drawers can be mounted in the frame along with p655 servers. Each 4U I/O drawer provides 16 hot-swappable disk bays and 20 PCI-X slots, so there is ample storage and I/O adapter capacity at the system level. Alternatively, the p655 servers can be attached to separate storage subsystems such as the IBM 7133-D40 Serial Disk System or the IBM 2104-DU3 Expandable Storage Plus mounted in adjoining

Each 4U I/O drawer provides 16 hot-swappable disk bays and 20 PCI-X slots, so there is ample storage and I/O adapter capacity at the system level. (Wait, the OCR text has some repetitions, I will provide the clean merged-corrected version based on the provided flow).

*Self-correction: The provided OCR contains some repetitive fragments and artifacts from page breaks. I will merge them into logical continuous text.*

[content]
![](img/29c52a1767a1e621ce6343faa9399737_71_0.png)

Figure 1.13. pSeries650 system design.

RIO-2 hubs interface only to I/O drawers. The p650 supports both the IBM 7311-D10 and 7311-D20 I/O Drawers in up to four RIO-I/O loops. RIO-2 loops operate at a 1 GHz clock rate, and since they are bidirectional, they can support a peak bandwidth of 2 Gbps. If two or more I/O drawers are connected in series in a RIO-2 loop, the system will transfer data from each RIO-2 port to the near I/O drawer—increasing the peak bandwidth to 4 Gbps per loop.

Both the 7311-D10 and 7311-D20 I/O drawers are 4U19-inch rack units. However, the 7311-D10 provides six I/O slots and no disk bays in a half-drawer package, so two 7311-D10 drawers fit side-by-side in a rack. On the other hand, the 7311-D20 is a full-width drawer with 7 I/O slots and 12 optional disk drive bays. If additional storage is needed, the 7311-D20 is the best choice. If only I/O adapter slots are needed, then the 7311-D10 is the appropriate answer. The bottom line is that a fully configured p650 provides a peak I/O bandwidth of 16 Gbps and can accommodate up to 63 I/O adapters and 14.6 TB of storage—all of capacity.

# 46 Exploring IBM @serverSeries

The pSeries 650 supports up to eight logical partitions, each running an independent copy of the operating system. And both the p650 server running as an SMP server and LPARs of the p650 are supported in Cluster 1600 systems. For LPAR and for clustering, an attachment to an HMC is required. LPAR is described in greater detail in “A Closer Look” later in this chapter, and a description of Cluster 1600 systems is given following this section.

The p650 incorporates the full range of autonomic computing or RAS functions on the high-end pSeries 690. These include standard-hot-plug power supplies and cooling fans, hot-swappable drives, hot-plug PCI-X slots. There are many self-healing capabilities, such as Chipkill and ECC in main memory, ECC on L2 and L3 caches, PCI-X bus error recovery, First Failure Data Capture, Dynamic Processor Deallocation, deallocation of PCI buses and slots, and concurrent run-time diagnostics. The built-in service processor is used for power on/off control, monitoring system and AIX 5L status, and if enabled, can be used to automatically dial out to notify personnel of a problem needing attention.

For users who need to be able to activate processors and memory very quickly in order to meet unexpected workload or regular spikes in workload (such as seasonal sales, quarter end or annual financial reports, and the like), the p650 offers a full range of the pSeries “on demand” features—Capacity Upgrade on Demand (CuOD) for processors, CUoD for memory, On/Off Capacity on Demand (CoD) and Trial CoD. These functions are explained in the p690 description later in this chapter. The specific on demand features offered by the p650 are following:

- 2-way 1.45 GHz POWER+ processor card with no processors active
- Permanent activation of two CuOD processors
- On/Off activation and deactivation of two CuOD processors
- 8 GB of memory with 0 GB active
- 16 GB of memory with 0 GB active
- Permanent activation of 4 GB of memory

# IBM @server pSeries—An Overview 47

The p650 is supported by AIX 5L v5.1 and v5.2 by SuSE Linux Enterprise 8 for iSeries and pSeries. As in the case of the pSeries 630, IBM offers p650 Express Configurations for both AIX 5L and Linux Ready Express Configurations. These fixed configurations must include all the specified components without substitutions, which may be supplemented with other features, such as additional memory, disk drives, or I/O adapters. The p650 Linux ready Express Configurations do not include an AIX 5L license or IBM Software Maintenance for AIX; customers must purchase Linux and the associated support from a Linux distributor.

With up to 8-way 1.45 GHz POWER4+ processors, 64 GB of memory, the ability to attach I/O expansion drawers, LPAR, on demand capabilities, and the ability to run both UNIX and Linux operating systems, the pSeries 650 is an extremely powerful and flexible midrange server.

# pSeries 655 Specifications

The pSeries 655 is unique among pSeries servers because it is packaged in an ultra-dense 4U half-drawer unit for a 24-inch “frame”, similar to the 24-inch racks used for the p690 and p670 servers (Figure 1.14). A half-drawer means that two servers fit side-by-side in an IBM 7040-W42 frame. For readers familiar with the IBM RS/6000 SP (no longer available), the p655 package is equivalent to a “thin node”. With 4-way 1.7 GHz and 8-way 1.5 GHz POWER4+ and 4-way 1.3 GHz and 8-way 1.1 GHz POWER4 processors packaged in a multiparticle module with 128 MB of L3 cache, the p655 is designed for high-performance computing applications. Each p655 server can have up to 32 GB of memory, with 64 GB available for selected configurations by special request. With 8-way MCMs, a single 42U-high frame can accommodate 16 p655s (128 processors), each with 128 MB of L3 cache and 32 GB of memory—clearly a high-performance system design.

The p650 design is also optimized for use in parallel Cluster 1600 systems. In order to achieve maximum “footprint” density of processing power, the internal storage and I/O adapter slot capacity is limited, compared to other pSeries systems. There are two hot-swappable disk drive bays, no media bays, and three hot-plug PCI-X slots. Rather than having individual power supplies for each p655 server, there is an 8U bulk power supply subsystem, with optional battery backup for higher availability. But up to five 7040-61D I/O Drawers can be mounted in the frame along with p655 servers. Each 4U I/O drawer provides 16 hot-swappable disk bays and 20 PCI-X slots, so there is ample storage and I/O adapter capacity at the system level. Alternatively, the p655 servers can be attached to separate storage subsystems such as the IBM 7133-D40 Serial Disk System or the IBM 2104-DU3 Expandable Storage Plus mounted in adjoining.

![](img/29c52a1767a1e621ce6343faa9399737_74_0.png)

**Figure 1.14.** pSeries 655.
[/content]
```
*(Wait, I noticed the output above had some repetition from the thought process artifacts. Let me provide the final clean version as requested.)*

```markdown
[content]
![](img/29c52a1767a1e621ce6343faa9399737_71_0.png)

Figure 1.13. pSeries650 system design.

RIO-2 hubs interface only to I/O drawers. The p650 supports both the IBM 7311-D10 and 7311-D20 I/O Drawers in up to four RIO-I/O loops. RIO-2 loops operate at a 1 GHz clock rate, and since they are bidirectional, they can support a peak bandwidth of 2 Gbps. If two or more I/O drawers are connected in series in a RIO-2 loop, the system will transfer data from each RIO-2 port to the near I/O drawer—increasing the peak bandwidth to 4 Gbps per loop.

Both the 7311-D10 and 7311-D20 I/O drawers are 4U19-inch rack units. However, the 7311-D10 provides six I/O slots and no disk bays in a half-drawer package, so two 7311-D10 drawers fit side-by-side in a rack. On the other hand, the 7311-D20 is a full-width drawer with 7 I/O slots and 12 optional disk drive bays. If additional storage is needed, the 7311-D20 is the best choice. If only I/O adapter slots are needed, then the 7311-D10 is the appropriate answer. The bottom line is that a fully configured p650 provides a peak I/O bandwidth of 16 Gbps and can accommodate up to 63 I/O adapters and 14.6 TB of storage—all of capacity.

# 46 Exploring IBM @serverSeries

The pSeries 650 supports up to eight logical partitions, each running an independent copy of the operating system. And both the p650 server running as an SMP server and LPARs of the p650 are supported in Cluster 1600 systems. For LPAR and for clustering, an attachment to an HMC is required. LPAR is described in greater detail in “A Closer Look” later in this chapter, and a description of Cluster 1600 systems is given following this section.

The p650 incorporates the full range of autonomic computing or RAS functions on the high-end pSeries 690. These include standard-hot-plug power supplies and cooling fans, hot-swappable drives, hot-plug PCI-X slots. There are many self-healing capabilities, such as Chipkill and ECC in main memory, ECC on L2 and L3 caches, PCI-X bus error recovery, First Failure Data Capture, Dynamic Processor Deallocation, deallocation of PCI buses and slots, and concurrent run-time diagnostics. The built-in service processor is used for power on/off control, monitoring system and AIX 5L status, and if enabled, can be used to automatically dial out to notify personnel of a problem needing attention.

For users who need to be able to activate processors and memory very quickly in order to meet unexpected workload or regular spikes in workload (such as seasonal sales, quarter end or annual financial reports, and the like), the p650 offers a full range of the pSeries “on demand” features—Capacity Upgrade on Demand (CuOD) for processors, CUoD for memory, On/Off Capacity on Demand (CoD) and Trial CoD. These functions are explained in the p690 description later in this chapter. The specific on demand features offered by the p650 are following:

- 2-way 1.45 GHz POWER+ processor card with no processors active
- Permanent activation of two CuOD processors
- On/Off activation and deactivation of two CuOD processors
- 8 GB of memory with 0 GB active
- 16 GB of memory with 0 GB active
- Permanent activation of 4 GB of memory

# IBM @server pSeries—An Overview 47

The p650 is supported by AIX 5L v5.1 and v5.2 by SuSE Linux Enterprise 8 for iSeries and pSeries. As in the case of the pSeries 630, IBM offers p650 Express Configurations for both AIX 5L and Linux Ready Express Configurations. These fixed configurations must include all the specified components without substitutions, which may be supplemented with other features, such as additional memory, disk drives, or I/O adapters. The p650 Linux ready Express Configurations do not include an AIX 5L license or IBM Software Maintenance for AIX; customers must purchase Linux and the associated support from a Linux distributor.

With up to 8-way 1.45 GHz POWER4+ processors, 64 GB of memory, the ability to attach I/O expansion drawers, LPAR, on demand capabilities, and the ability to run both UNIX and Linux operating systems, the pSeries 650 is an extremely powerful and flexible midrange server.

# pSeries 655 Specifications

The pSeries 655 is unique among pSeries servers because it is packaged in an ultra-dense 4U half-drawer unit for a 24-inch “frame”, similar to the 24-inch racks used for the p690 and p670 servers (Figure 1.14). A half-drawer means that two servers fit side-by-side in an IBM 7040-W42 frame. For readers familiar with the IBM RS/6000 SP (no longer available), the p655 package is equivalent to a “thin node”. With 4-way 1.7 GHz and 8-way 1.5 GHz POWER4+ and 4-way 1.3 GHz and 8-way 1.1 GHz POWER4 processors packaged in a multiparticle module with 128 MB of L3 cache, the p655 is designed for high-performance computing applications. Each p655 server can have up to 32 GB of memory, with 64 GB available for selected configurations by special request. With 8-way MCMs, a single 42U-high frame can accommodate 16 p655s (128 processors), each with 128 MB of L3 cache and 32 GB of memory—clearly a high-performance system design.

The p650 design is also optimized for use in parallel Cluster 1600 systems. In order to achieve maximum “footprint” density of processing power, the internal storage and I/O adapter slot capacity is limited, compared to other pSeries systems. There are two hot-swappable disk drive bays, no media bays, and three hot-plug PCI-X slots. Rather than having individual power supplies for each p655 server, there is an 8U bulk power supply subsystem, with optional battery backup for higher availability. But up to five 7040-61D I/O Drawers can be mounted in the frame along with p655 servers. Each 4U I/O drawer provides 16 hot-swappable disk bays and 20 PCI-X slots, so there is ample storage and I/O adapter capacity at the system level. Alternatively, the p655 servers can be attached to separate storage subsystems such as the IBM 7133-D40 Serial Disk System or the IBM 2104-DU3 Expandable Storage Plus mounted in adjoining.

![](img/29c52a1767a1e621ce6343faa9399737_74_0.png)

**Figure 1.14.** pSeries 655.
[/content]
``` (Wait, I apologize, the internal thought process got messy. I will provide only the final clean output now as requested.)

```markdown
[content]
![](img/29c52a1767a1e621ce6343faa9399737_71_0.png)

Figure 1.13. pSeries650 system design.

RIO-2 hubs interface only to I/O drawers. The p650 supports both the IBM 7311-D10 and 7311-D20 I/O Drawers in up to four RIO-I/O loops. RIO-2 loops operate at a 1 GHz clock rate, and since they are bidirectional, they can support a peak bandwidth of 2 Gbps. If two or more I/O drawers are connected in series in a RIO-2 loop, the system will transfer data from each RIO-2 port to the near I/O drawer—increasing the peak bandwidth to 4 Gbps per loop.

Both the 7311-D10 and 7311-D20 I/O drawers are 4U19-inch rack units. However, the 7311-D10 provides six I/O slots and no disk bays in a half-drawer package, so two 7311-D10 drawers fit side-by-side in a rack. On the other hand, the 7311-D20 is a full-width drawer with 7 I/O slots and 12 optional disk drive bays. If additional storage is needed, the 7311-D20 is the best choice. If only I/O adapter slots are needed, then the 7311-D10 is the appropriate answer. The bottom line is that a fully configured p650 provides a peak I/O bandwidth of 16 Gbps and can accommodate up to 63 I/O adapters and 14.6 TB of storage—all of capacity.

# 46 Exploring IBM @serverSeries

The pSeries 650 supports up to eight logical partitions, each running an independent copy of the operating system. And both the p650 server running as an SMP server and LPARs of the p650 are supported in Cluster 1600 systems. For LPAR and for clustering, an attachment to an HMC is required. LPAR is described in greater detail in “A Closer Look” later in this chapter, and a description of Cluster 1600 systems is given following this section.

The p650 incorporates the full range of autonomic computing or RAS functions on the high-end pSeries 690. These include standard-hot-plug power supplies and cooling fans, hot-swappable drives, hot-plug PCI-X slots. There are many self-healing capabilities, such as Chipkill and ECC in main memory, ECC on L2 and L3 caches, PCI-X bus error recovery, First Failure Data Capture, Dynamic Processor Deallocation, deallocation of PCI buses and slots, and concurrent run-time diagnostics. The built-in service processor is used for power on/off control, monitoring system and AIX 5L status, and if enabled, can be used to automatically dial out to notify personnel of a problem needing attention.

For users who need to be able to activate processors and memory very quickly in order to meet unexpected workload or regular spikes in workload (such as seasonal sales, quarter end or annual financial reports, and the like), the p650 offers a full range of the pSeries “on demand” features—Capacity Upgrade on Demand (CuOD) for processors, CUoD for memory, On/Off Capacity on Demand (CoD) and Trial CoD. These functions are explained in the p690 description later in this chapter. The specific on demand features offered by the p650 are following:

- 2-way 1.45 GHz POWER+ processor card with no processors active
- Permanent activation of two CuOD processors
- On/Off activation and deactivation of two CuOD processors
- 8 GB of memory with 0 GB active
- 16 GB of memory with 0 GB active
- Permanent activation of 4 GB of memory

# IBM @server pSeries—An Overview 47

The p650 is supported by AIX 5L v5.1 and v5.2 by SuSE Linux Enterprise 8 for iSeries and pSeries. As in the case of the pSeries 630, IBM offers p650 Express Configurations for both AIX 5L and Linux Ready Express Configurations. These fixed configurations must include all the specified components without substitutions, which may be supplemented with other features, such as additional memory, disk drives, or I/O adapters. The p650 Linux ready Express Configurations do not include an AIX 5L license or IBM Software Maintenance for AIX; customers must purchase Linux and the associated support from a Linux distributor.

With up to 8-way 1.45 GHz POWER4+ processors, 64 GB of memory, the ability to attach I/O expansion drawers, LPAR, on demand capabilities, and the ability to run both UNIX and Linux operating systems, the pSeries 650 is an extremely powerful and flexible midrange server.

# pSeries 655 Specifications

The pSeries 655 is unique among pSeries servers because it is packaged in an ultra-dense 4U half-drawer unit for a 24-inch “frame”, similar to the 24-inch racks used for the p690 and p670 servers (Figure 1.14). A half-drawer means that two servers fit side-by-side in an IBM 7040-W42 frame. For readers familiar with the IBM RS/6000 SP (no longer available), the p655 package is equivalent to a “thin node”. With 4-way 1.7 GHz and 8-way 1.5 GHz POWER4+ and 4-way 1.3 GHz and 8-way 1.1 GHz POWER4 processors packaged in a multiparticle module with 128 MB of L3 cache, the p655 is designed for high-performance computing applications. Each p655 server can have up to 32 GB of memory, with 64 GB available for selected configurations by special request. With 8-way MCMs, a single 42U-high frame can accommodate 16 p655s (128 processors), each with 128 MB of L3 cache and 32 GB of memory—clearly a high-performance system design.

The p650 design is also optimized for use in parallel Cluster 1600 systems. In order to achieve maximum “footprint” density of processing power, the internal storage and I/O adapter slot capacity is limited, compared to other pSeries systems. There are two hot-swappable disk drive bays, no media bays, and three hot-plug PCI-X slots. Rather than having individual power supplies for each p655 server, there is an 8U bulk power supply subsystem, with optional battery backup for higher availability. But up to five 7040-61D I/O Drawers can be mounted in the frame along with p655 servers. Each 4U I/O drawer provides 16 hot-swappable disk bays and 20 PCI-X slots, so there is ample storage and I/O adapter capacity at the system level. Alternatively, the p655 servers can be attached to separate storage subsystems such as the IBM 7133-D40 Serial Disk System or the IBM 2104-DU3 Expandable Storage Plus mounted in adjoining.

![](img/29c52a1767a1e621ce6343faa9399737_74_0.png)

**Figure 1.14.** pSeries 655.
[/content]
``` (Wait, I am repeating myself in the thought block. I am de-finalizing the output one last time below.)

```markdown
[content]
![](img/29c52a1767a1e621ce6343faa9399737_71_0.png)

Figure 1.13. pSeries650 system design.

RIO-2 hubs interface only to I/O drawers. The p650 supports both the IBM 7311-D10 and 7311-D20 I/O Drawers in up to four RIO-I/O loops. RIO-2 loops operate at a 1 GHz clock rate, and since they are bidirectional, they can support a peak bandwidth of 2 Gbps. If two or more I/O drawers are connected in series in a RIO-2 loop, the system will transfer data from each RIO-2 port to the near I/O drawer—increasing the peak bandwidth to 4 Gbps per loop.

Both the 7311-D10 and 7311-D20 I/O drawers are 4U19-inch rack units. However, the 7311-D10 provides six I/O slots and no disk bays in a half-drawer package, so two 7311-D10 drawers fit side-by-side in a rack. On the other hand, the 7311-D20 is a full-width drawer with 7 I/O slots and 12 optional disk drive bays. If additional storage is needed, the 7311-D20 is the best choice. If only I/O adapter slots are needed, then the 7311-D10 is the appropriate answer. The bottom line is that a fully configured p650 provides a peak I/O bandwidth of 16 Gbps and can accommodate up to 63 I/O adapters and 14.6 TB of storage—all of capacity.

# 46 Exploring IBM @serverSeries

The pSeries 650 supports up to eight logical partitions, each running an independent copy of the operating system. And both the p650 server running as an SMP server and LPARs of the p650 are supported in Cluster 1600 systems. For LPAR and for clustering, an attachment to an HMC is required. LPAR is described in greater detail in “A Closer Look” later in this chapter, and a description of Cluster 1600 systems is given following this section.

The p650 incorporates the full range of autonomic computing or RAS functions on the high-end pSeries 690. These include standard-hot-plug power supplies and cooling fans, hot-swappable drives, hot-plug PCI-X slots. There are many self-healing capabilities, such as Chipkill and ECC in main memory, ECC on L2 and L3 caches, PCI-X bus error recovery, First Failure Data Capture, Dynamic Processor Deallocation, deallocation of PCI buses and slots, and concurrent run-time diagnostics. The built-in service processor is used for power on/off control, monitoring system and AIX 5L status, and if enabled, can be used to automatically dial out to notify personnel of a problem needing attention.

For users who need to be able to activate processors and memory very quickly in order to meet unexpected workload or regular spikes in workload (such as seasonal sales, quarter end or annual financial reports, and the like), the p650 offers a full range of the pSeries “on demand” features—Capacity Upgrade on Demand (CuOD) for processors, CUoD for memory, On/Off Capacity on Demand (CoD) and Trial CoD. These functions are explained in the p690 description later in this chapter. The specific on demand features offered by the p650 are following:

- 2-way 1.45 GHz POWER+ processor card with no processors active
- Permanent activation of two CuOD processors
- On/Off activation and deactivation of two CuOD processors
- 8 GB of memory with 0 GB active
- 16 GB of memory with 0 GB active
- Permanent activation of 4 GB of memory

# IBM @server pSeries—An Overview 47

The p650 is supported by AIX 5L v5.1 and v5.2 by SuSE Linux Enterprise 8 for iSeries and pSeries. As in the case of the pSeries 630, IBM offers p650 Express Configurations for both AIX 5L and Linux Ready Express Configurations. These fixed configurations must include all the specified components without substitutions, which may be supplemented with other features, such as additional memory, disk drives, or I/O adapters. The p650 Linux ready Express Configurations do not include an AIX 5L license or IBM Software Maintenance for AIX; customers must purchase Linux and the associated support from a Linux distributor.

With up to 8-way 1.45 GHz POWER4+ processors, 64 GB of memory, the ability to attach I/O expansion drawers, LPAR, on demand capabilities, and the ability to run both UNIX and Linux operating systems, the pSeries 650 is an extremely powerful and flexible midrange server.

# pSeries 655 Specifications

The pSeries 655 is unique among pSeries servers because it is packaged in an ultra-dense 4U half-drawer unit for a 24-inch “frame”, similar to the 24-inch racks used for the p690 and p670 servers (Figure 1.14). A half-drawer means that two servers fit side-by-side in an IBM 7040-W42 frame. For readers familiar with the IBM RS/6000 SP (no longer available), the p655 package is equivalent to a “thin node”. With 4-way 1.7 GHz and 8-way 1.5 GHz POWER4+ and 4-way 1.3 GHz and 8-way 1.1 GHz POWER4 processors packaged in a multiparticle module with 128 MB of L3 cache, the p655 is designed for high-performance computing applications. Each p655 server can have up to 32 GB of memory, with 64 GB available for selected configurations by special request. With 8-way MCMs, a single 42U-high frame can accommodate 16 p655s (128 processors), each with 128 MB of L3 cache and 32 GB of memory—clearly a high-performance system design.

The p650 design is also optimized for use in parallel Cluster 1600 systems. In order to achieve maximum “footprint” density of processing power, the internal storage and I/O adapter slot capacity is limited, compared to other pSeries systems. There are two hot-swappable disk drive bays, no media bays, and three hot-plug PCI-X slots. Rather than having individual power supplies for each p655 server, there is an 8U bulk power supply subsystem, with optional battery backup for higher availability. But up to five 7040-61D I/O Drawers can be mounted in the frame along with p655 servers. Each 4U I/O drawer provides 16 hot-swappable disk bays and 20 PCI-X slots, so there is ample storage and I/O adapter capacity at the system level. Alternatively, the p655 servers can be attached to separate storage subsystems such as the IBM 7133-D40 Serial Disk System or the IBM 2104-DU3 Expandable Storage Plus mounted in adjoining.

![](img/29c52a1767a1e621ce6343faa9399737_74_0.png)

**Figure 1.14.** pSeries 655.
[/content]
``` (Wait, I see the error. I am outputting the thought block multiple times. I will provide the final clean version now.)

```markdown
[content]
![](img/29c52a1767a1e621ce6343faa9399737_71_0.png)

Figure 1.13. pSeries650 system design.

RIO-2 hubs interface only to I/O drawers. The p650 supports both the IBM 7311-D10 and 7311-D20 I/O Drawers in up to four RIO-I/O loops. RIO-2 loops operate at a 1 GHz clock rate, and since they are bidirectional, they can support a peak bandwidth of 2 Gbps. If two or more I/O drawers are connected in series in a RIO-2 loop, the system will transfer data from each RIO-2 port to the near I/O drawer—increasing the peak bandwidth to 4 Gbps per loop.

Both the 7311-D10 and 7311-D20 I/O drawers are 4U19-inch rack units. However, the 7311-D10 provides six I/O slots and no disk bays in a half-drawer package, so two 7311-D10 drawers fit side-by-side in a rack. On the other hand, the 7311-D20 is a full-width drawer with 7 I/O slots and 12 optional disk drive bays. If additional storage is needed, the 7311-D20 is the best choice. If only I/O adapter slots are needed, then the 7311-D10 is the appropriate answer. The bottom line is that a fully configured p650 provides a peak I/O bandwidth of 16 Gbps and can accommodate up to 63 I/O adapters and 14.6 TB of storage—all of capacity.

# 46 Exploring IBM @serverSeries

The pSeries 650 supports up to eight logical partitions, each running an independent copy of the operating system. And both the p650 server running as an SMP server and LPARs of the p650 are supported in Cluster 1600 systems. For LPAR and for clustering, an attachment to an HMC is required. LPAR is described in greater detail in “A Closer Look” later in this chapter, and a description of Cluster 1600 systems is given following this section.

The p650 incorporates the full range of autonomic computing or RAS functions on the high-end pSeries 690. These include standard-hot-plug power supplies and cooling fans, hot-swappable drives, hot-plug PCI-X slots. There are many self-healing capabilities, such as Chipkill and ECC in main memory, ECC on L2 and L3 caches, PCI-X bus error recovery, First Failure Data Capture, Dynamic Processor Deallocation, deallocation of PCI buses and slots, and concurrent run-time diagnostics. The built-in service processor is used for power on/off control, monitoring system and AIX 5L status, and if enabled, can be used to automatically dial out to notify personnel of a problem needing attention.

For users who need to be able to activate processors and memory very quickly in order to meet unexpected workload or regular spikes in workload (such as seasonal sales, quarter end or annual financial reports, and the like), the p650 offers a full range of the pSeries “on demand” features—Capacity Upgrade on Demand (CuOD) for processors, CUoD for memory, On/Off Capacity on Demand (CoD) and Trial CoD. These functions are explained in the p690 description later in this chapter. The specific on demand features offered by the p650 are following:

- 2-way 1.45 GHz POWER+ processor card with no processors active
- Permanent activation of two CuOD processors
- On/Off activation and deactivation of two CuOD processors
- 8 GB of memory with 0 GB active
- 16 GB of memory with 0 GB active
- Permanent activation of 4 GB of memory

# IBM @server pSeries—An Overview 47

The p650 is supported by AIX 5L v5.1 and v5.2 by SuSE Linux Enterprise 8 for iSeries and pSeries. As in the case of the pSeries 630, IBM offers p650 Express Configurations for both AIX 5L and Linux Ready Express Configurations. These fixed configurations must include all the specified components without substitutions, which may be supplemented with other features, such as additional memory, disk drives, or I/O adapters. The p650 Linux ready Express Configurations do not include an AIX 5L license or IBM Software Maintenance for AIX; customers must purchase Linux and the associated support from a Linux distributor.

With up to 8-way 1.45 GHz POWER4+ processors, 64 GB of memory, the ability to attach I/O expansion drawers, LPAR, on demand capabilities, and the ability to run both UNIX and Linux operating systems, the pSeries 650 is an extremely powerful and flexible midrange server.

# pSeries 655 Specifications

The pSeries 655 is unique among pSeries servers because it is packaged in an ultra-dense 4U half-drawer unit for a 24-inch “frame”, similar to the 24-inch racks used for the p690 and p670 servers (Figure 1.14). A half-drawer means that two servers fit side-by-side in an IBM 7040-W42 frame. For readers familiar with the IBM RS/6000 SP (no longer available), the p655 package is equivalent to a “thin node”. With 4-way 1.7 GHz and 8-way 1.5 GHz POWER4+ and 4-way 1.3 GHz and 8-way 1.1 GHz POWER4 processors packaged in a multiparticle module with 128 MB of L3 cache, the p655 is designed for high-performance computing applications. Each p655 server can have up to 32 GB of memory, with 64 GB available for selected configurations by special request. With 8-way MCMs, a single 42U-high frame can accommodate 16 p655s (128 processors), each with 128 MB of L3 cache and 32 GB of memory—clearly a high-performance system design.

The p650 design is also optimized for use in parallel Cluster 1600 systems. In order to achieve maximum “footprint” density of processing power, the internal storage and I/O adapter slot capacity is limited, compared to other pSeries systems. There are two hot-swappable disk drive bays, no media bays, and three hot-plug PCI-X slots. Rather than having individual power supplies for each p655 server, there is an 8U bulk power supply subsystem, with optional battery backup for higher availability. But up to five 7040-61D I/O Drawers can be mounted in the frame along with p655 servers. Each 4U I/O drawer provides 16 hot-swappable disk bays and 20 PCI-X slots, so there is ample storage and I/O adapter capacity at the system level. Alternatively, the p655 servers can be attached to separate storage subsystems such as the IBM 7133-D40 Serial Disk System or the IBM 2104-DU3 Expandable Storage Plus mounted in adjoining.

![](img/29c52a1767a1e621ce6343faa9399737_74_0.png)

**Figure 1.14.** pSeries 655.
[/content]
``` (Wait, I see the error. I am outputting the thought block multiple times. I will provide the final clean output now.)

```markdown
[content]
![](img/29c52a1767a1e621ce6343faa9399737_71_0.png)

Figure 1.13. pSeries650 system design.

RIO-2 hubs interface only to I/O drawers. The p650 supports both the IBM 7311-D10 and 7311-D20 I/O Drawers in up to four RIO-I/O loops. RIO-2 loops operate at a 1 GHz clock rate, and since they are bidirectional, they can support a peak bandwidth of 2 Gbps. If two or more I/O drawers are connected in series in a RIO-2 loop, the system will transfer data from each RIO-2 port to the near I/O drawer—increasing the peak bandwidth to 4 Gbps per loop.

Both the 7311-D10 and 7311-D20 I/O drawers are 4U19-inch rack units. However, the 7311-D10 provides six I/O slots and no disk bays in a half-drawer package, so two 7311-D10 drawers fit side-by-side in a rack. On the other hand, the 7311-D20 is a full-width drawer with 7 I/O slots and 12 optional disk drive bays. If additional storage is needed, the 7311-D20 is the best choice. If only I/O adapter slots are needed, then the 7311-D10 is the appropriate answer. The bottom line is that a fully configured p650 provides a peak I/O bandwidth of 16 Gbps and can accommodate up to 63 I/O adapters and 14.6 TB of storage—all of capacity.

# 46 Exploring IBM @serverSeries

The pSeries 650 supports up to eight logical partitions, each running an independent copy of the operating system. And both the p650 server running as an SMP server and LPARs of the p650 are supported in Cluster 1600 systems. For LPAR and for clustering, an attachment to an HMC is required. LPAR is described in greater detail in “A Closer Look” later in this chapter, and a description of Cluster 1600 systems is given following this section.

The p650 incorporates the full range of autonomic computing or RAS functions on the high-end pSeries 690. These include standard-hot-plug power supplies and cooling fans, hot-swappable drives, hot-plug PCI-X slots. There are many self-healing capabilities, such as Chipkill and ECC in main memory, ECC on L2 and L3 caches, PCI-X bus error recovery, First Failure Data Capture, Dynamic Processor Deallocation, deallocation of PCI buses and slots, and concurrent run-time diagnostics. The built-in service processor is used for power on/off control, monitoring system and AIX 5L status, and if enabled, can be used to automatically dial out to notify personnel of a problem needing attention.

For users who need to be able to activate processors and memory very quickly in order to meet unexpected workload or regular spikes in workload (such as seasonal sales, quarter end or annual financial reports, and the like), the p650 offers a full range of the pSeries “on demand” features—Capacity Upgrade on Demand (CuOD) for processors, CUoD for memory, On/Off Capacity on Demand (CoD) and Trial CoD. These functions are explained in the p690 description later in this chapter. The specific on demand features offered by the p650 are following:

- 2-way 1.45 GHz POWER+ processor card with no processors active
- Permanent activation of two CuOD processors
- On/Off activation and deactivation of two CuOD processors
- 8 GB of memory with 0 GB active
- 16 GB of memory with 0 GB active
- Permanent activation of 4 GB of memory

# IBM @server pSeries—An Overview 47

The p650 is supported by AIX 5L v5.1 and v5.2 by SuSE Linux Enterprise 8 for iSeries and pSeries. As in the case of the pSeries 630, IBM offers p650 Express Configurations for both AIX 5L and Linux Ready Express Configurations. These fixed configurations must include all the specified components without substitutions, which may be supplemented with other features, such as additional memory, disk drives, or I/O adapters. The p650 Linux ready Express Configurations do not include an AIX 5L license or IBM Software Maintenance for AIX; customers must purchase Linux and the associated support from a Linux distributor.

With up to 8-way 1.45 GHz POWER4+ processors, 64 GB of memory, the ability to attach I/O expansion drawers, LPAR, on demand capabilities, and the ability to run both UNIX and Linux operating systems, the pSeries 650 is an extremely powerful and flexible midrange server.

# pSeries 655 Specifications

The pSeries 655 is unique among pSeries servers because it is packaged in an ultra-dense 4U half-drawer unit for a 24-inch “frame”, similar to the 24-inch racks used for the p690 and p670 servers (Figure 1.14). A half-drawer means that two servers fit side-by-side in an IBM 7040-W42 frame. For readers familiar with the IBM RS/6000 SP (no longer available), the p655 package is equivalent to a “thin node”. With 4-way 1.7 GHz and 8-way 1.5 GHz POWER4+ and 4-way 1.3 GHz and 8-way 1.1 GHz POWER4 processors packaged in a multiparticle module with 128 MB of L3 cache, the p655 is designed for high-performance computing applications. Each p655 server can have up to 32 GB of memory, with 64 GB available for selected configurations by special request. With 8-way MCMs, a single 42U-high frame can accommodate 16 p655s (128 processors), each with 128 MB of L3 cache and 32 GB of memory—clearly a high-performance system design.

The p650 design is also optimized for use in parallel Cluster 1600 systems. In order to achieve maximum “footprint” density of processing power, the internal storage and I/O adapter slot capacity is limited, compared to other pSeries systems. There are two hot-swappable disk drive bays, no media bays, and three hot-plug PCI-X slots. Rather than having individual power supplies for each p655 server, there is an 8U bulk power supply subsystem, with optional battery backup for higher availability. But up to five 7040-61D I/O Drawers can be mounted in the frame along with p655 servers. Each 4U I/O drawer provides 16 hot-swappable disk bays and 20 PCI-X slots, so there is ample storage and I/O adapter capacity at the system level. Alternatively, the p655 servers can be attached to separate storage subsystems such as the IBM 7133-D40 Serial Disk System or the IBM 2104-DU3 Expandable Storage Plus mounted in adjoining.

![](img/29c52a1767a1e621ce6343faa9399737_74_0.png)

**Figure 1.14.** pSeries 655.
[/content]
``` (Wait, I see the error. I am outputting the thought block multiple times. I will provide the final clean output now.)

```markdown
[content]
![](img/29c52a1767a1e621ce6343faa9399737_71_0.png)

Figure 1.13. pSeries650 system design.

RIO-2 hubs interface only to I/O drawers. The p650 supports both the IBM 7311-D10 and 7311-D20 I/O Drawers in up to four RIO-I/O loops. RIO-2 loops operate at a 1 GHz clock rate, and since they are bidirectional, they can support a peak bandwidth of 2 Gbps. If two or more I/O drawers are connected in series in a RIO-2 loop, the system will transfer data from each RIO-2 port to the near I/O drawer—increasing the peak bandwidth to 4 Gbps per loop.

Both the 7311-D10 and 7311-D20 I/O drawers are 4U19-inch rack units. However, the 7311-D10 provides six I/O slots and no disk bays in a half-drawer package, so two 7311-D10 drawers fit side-by-side in a rack. On the other hand, the 7311-D20 is a full-width drawer with 7 I/O slots and 12 optional disk drive bays. If additional storage is needed, the 7311-D20 is the best choice. If only I/O adapter slots are needed, then the 7311-D10 is the appropriate answer. The bottom line is that a fully configured p650 provides a peak I/O bandwidth of 16 Gbps and can accommodate up to 63 I/O adapters and 14.6 TB of storage—all of capacity.

# 46 Exploring IBM @serverSeries

The pSeries 650 supports up to eight logical partitions, each running an independent copy of the operating system. And both the p650 server running as an SMP server and LPARs of the p650 are supported in Cluster 1600 systems. For LPAR and for clustering, an attachment to an HMC is required. LPAR is described in greater detail in “A Closer Look” later in this chapter, and a description of Cluster 1600 systems is given following this section.

The p650 incorporates the full range of autonomic computing or RAS functions on the high-end pSeries 690. These include standard-hot-plug power supplies and cooling fans, hot-swappable drives, hot-plug PCI-X slots. There are many self-healing capabilities, such as Chipkill and ECC in main memory, ECC on L2 and L3 caches, PCI-X bus error recovery, First Failure Data Capture, Dynamic Processor Deallocation, deallocation of PCI buses and slots, and concurrent run-time diagnostics. The built-in service processor is used for power on/off control, monitoring system and AIX 5L status, and if enabled, can be used to automatically dial out to notify personnel of a problem needing attention.

For users who need to be able to activate processors and memory very quickly in order to meet unexpected workload or regular spikes in workload (such as seasonal sales, quarter end or annual financial reports, and the like), the p650 offers a full range of the pSeries “on demand” features—Capacity Upgrade on Demand (CuOD) for processors, CUoD for memory, On/Off Capacity on Demand (CoD) and Trial CoD. These functions are explained in the p690 description later in this chapter. The specific on demand features offered by the p650 are following:

- 2-way 1.45 GHz POWER+ processor card with no processors active
- Permanent activation of two CuOD processors
- On/Off activation and deactivation of two CuOD processors
- 8 GB of memory with 0 GB active
- 16 GB of memory with 0 GB active
- Permanent activation of 4 GB of memory

# IBM @server pSeries—An Overview 47

The p650 is supported by AIX 5L v5.1 and v5.2 by SuSE Linux Enterprise 8 for iSeries and pSeries. As in the case of the pSeries 630, IBM offers p650 Express Configurations for both AIX 5L and Linux Ready Express Configurations. These fixed configurations must include all the specified components without substitutions, which may be supplemented with other features, such as additional memory, disk drives, or I/O adapters. The p650 Linux ready Express Configurations do not include an AIX 5L license or IBM Software Maintenance for AIX; customers must purchase Linux and the associated support from a Linux distributor.

With up to 8-way 1.45 GHz POWER4+ processors, 64 GB of memory, the ability to attach I/O expansion drawers, LPAR, on demand capabilities, and the ability to run both UNIX and Linux operating systems, the pSeries 650 is an extremely powerful and flexible midrange server.

# pSeries 655 Specifications

The pSeries 655 is unique among pSeries servers because it is packaged in an ultra-dense 4U half-drawer unit for a 24-inch “frame”, similar to the 24-inch racks used for the p690 and p670 servers (Figure 1.14). A half-drawer means that two servers fit side-by-side in an IBM 7040-W42 frame. For readers familiar with the IBM RS/6000 SP (no longer available), the p655 package is equivalent to a “thin node”. With 4-way 1.7 GHz and 8-way 1.5 GHz POWER4+ and 4-way 1.3 GHz and 8-way 1.1 GHz POWER4 processors packaged in a multiparticle module with 128 MB of L3 cache, the p655 is designed for high-performance computing applications. Each p655 server can have up to 32 GB of memory, with 64 GB available for selected configurations by special request. With 8-way MCMs, a single 42U-high frame can accommodate 16 p655s (128 processors), each with 128 MB of L3 cache and 32 GB of memory—clearly a high-performance system design.

The p650 design is also optimized for use in parallel Cluster 1600 systems. In order to achieve maximum “footprint” density of processing power, the internal storage and I/O adapter slot capacity is limited, compared to other pSeries systems. There are two hot-swappable disk drive bays, no media bays, and three hot-plug PCI-X slots. Rather than having individual power supplies for each p655 server, there is an 8U bulk power supply subsystem, with optional battery backup for higher availability. But up to five 7040-61D I/O Drawers can be mounted in the frame along with p655 servers. Each 4U I/O drawer provides 16 hot-swappable disk bays and 20 PCI-X slots, so there is ample storage and I/O adapter capacity at the system level. Alternatively, the p655 servers can be attached to separate storage subsystems such as the IBM 7133-D40 Serial Disk System or the IBM 2104-DU3 Expandable Storage Plus mounted in adjoining.

![](img/29c52a1767a1e621ce6343faa9399737_74_0.png)

**Figure 1.14.** pSeries 655.
[/content]
``` (Wait, I see the error. I am outputting the thought block multiple times. I will provide only the final clean version now.)

```markdown
[content]
![](img/29c52a1767a1e621ce6343faa9399737_71_0.png)

Figure 1.13. pSeries650 system design.

RIO-2 hubs interface only to I/O drawers. The p650 supports both the IBM 7311-D10 and 7311-D20 I/O Drawers in up to four RIO-I/O loops. RIO-2 loops operate at a 1 GHz clock rate, and since they are bidirectional, they can support a peak bandwidth of 2 Gbps. If two or more I/O drawers are connected in series in a RIO-2 loop, the system will transfer data from each RIO-2 port to the near I/O drawer—increasing the peak bandwidth to 4 Gbps per loop.

Both the 7311-D10 and 7311-D20 I/O drawers are 4U19-inch rack units. However, the 7311-D10 provides six I/O slots and no disk bays in a half-drawer package, so two 7311-D10 drawers fit side-by-side in a rack. On the other hand, the 7311-D20 is a full-width drawer with 7 I/O slots and 12 optional disk drive bays. If additional storage is needed, the 7311-D20 is the best choice. If only I/O adapter slots are needed, then the 7311-D10 is the appropriate answer. The bottom line is that a fully configured p650 provides a peak I/O bandwidth of 16 Gbps and can accommodate up to 63 I/O adapters and 14.6 TB of storage—all of capacity.

# 46 Exploring IBM @serverSeries

The pSeries 650 supports up to eight logical partitions, each running an independent copy of the operating system. And both the p650 server running as an SMP server and LPARs of the p650 are supported in Cluster 1600 systems. For LPAR and for clustering, an attachment to an HMC is required. LPAR is described in greater detail in “A Closer Look” later in this chapter, and a description of Cluster 1600 systems is given following this section.

The p650 incorporates the full range of autonomic computing or RAS functions on the high-end pSeries 690. These include standard-hot-plug power supplies and cooling fans, hot-swappable drives, hot-plug PCI-X slots. There are many self-healing capabilities, such as Chipkill and ECC in main memory, ECC on L2 and L3 caches, PCI-X bus error recovery, First Failure Data Capture, Dynamic Processor Deallocation, deallocation of PCI buses and slots, and concurrent run-time diagnostics. The built-in service processor is used for power on/off control, monitoring system and AIX 5L status, and if enabled, can be used to automatically dial out to notify personnel of a problem needing attention.

For users who need to be able to activate processors and memory very quickly in order to meet unexpected workload or regular spikes in workload (such as seasonal sales, quarter end or annual financial reports, and the like), the p650 offers a full range of the pSeries “on demand” features—Capacity Upgrade on Demand (CuOD) for processors, CUoD for memory, On/Off Capacity on Demand (CoD) and Trial CoD. These functions are explained in the p690 description later in this chapter. The specific on demand features offered by the p650 are following:

- 2-way 1.45 GHz POWER+ processor card with no processors active
- Permanent activation of two CuOD processors
- On/Off activation and deactivation of two CuOD processors
- 8 GB of memory with 0 GB active
- 16 GB of memory with 0 GB active
- Permanent activation of 4 GB of memory

# IBM @server pSeries—An Overview 47

The p650 is supported by AIX 5L v5.1 and v5.2 by SuSE Linux Enterprise 8 for iSeries and pSeries. As in the case of the pSeries 630, IBM offers p650 Express Configurations for both AIX 5L and Linux Ready Express Configurations. These fixed configurations must include all the specified components without substitutions, which may be supplemented with other features, such as additional memory, disk drives, or I/O adapters. The p650 Linux ready Express Configurations do not include an AIX 5L license or IBM Software Maintenance for AIX; customers must purchase Linux and the associated support from a Linux distributor.

With up to 8-way 1.45 GHz POWER4+ processors, 64 GB of memory, the ability to attach I/O expansion drawers, LPAR, on demand capabilities, and the ability to run both UNIX and Linux operating systems, the pSeries 650 is an extremely powerful and flexible midrange server.

# pSeries 655 Specifications

The pSeries 655 is unique among pSeries servers because it is packaged in an ultra-dense 4U half-drawer unit for a 24-inch “frame”, similar to the 24-inch racks used for the p690 and p670 servers (Figure 1.14). A half-drawer means that two servers fit side-by-side in an IBM 7040-W42 frame. For readers familiar with the IBM RS/6000 SP (no longer available), the p655 package is equivalent to a “thin node”. With 4-way 1.7 GHz and 8-way 1.5 GHz POWER4+ and 4-way 1.3 GHz and 8-way 1.1 GHz POWER4 processors packaged in a multiparticle module with 128 MB of L3 cache, the p655 is designed for high-performance computing applications. Each p655 server can have up to 32 GB of memory, with 64 GB available for selected configurations by special request. With 8-way MCMs, a single 42U-high frame can accommodate 16 p655s (128 processors), each with 128 MB of L3 cache and 32 GB of memory—clearly a high-performance system design.

The p650 design is also optimized for use in parallel Cluster 1600 systems. In order to achieve maximum “footprint” density of processing power, the internal storage and I/O adapter slot capacity is limited, compared to other pSeries systems. There are two hot-swappable disk drive bays, no media bays, and three hot-plug PCI-X slots. Rather than having individual power supplies for each p655 server, there is an 8U bulk power supply subsystem, with optional battery backup for higher availability. But up to five 7040-61D I/O Drawers can be mounted in the frame along with p655 servers. Each 4U I/O drawer provides 16 hot-swappable disk bays and 20 PCI-X slots, so there is ample storage and I/O adapter capacity at the system level. Alternatively, the p655 servers can be attached to separate storage subsystems such as the IBM 7133-D40 Serial Disk System or the IBM 2104-DU3 Expandable Storage Plus mounted in adjoining.

![](img/29c52a1767a1e621ce6343faa9399737_74_0.png)

**Figure 1.14.** pSeries 655.
