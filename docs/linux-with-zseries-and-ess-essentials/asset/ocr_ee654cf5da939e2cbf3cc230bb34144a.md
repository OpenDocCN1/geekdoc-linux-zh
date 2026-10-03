# Remote copy

The ESS Model 800 supports two types of Remote Copy, Peer-to-Peer Remote Copy (PPRC), and Extended Remote Copy (XRC). PPRC is a hardware-based solution for mirroring logical volumes from a primary site (the application site) onto the volumes of a secondary site (the recovery site), using either a synchronous or non-synchronous process. PPRC is a Remote Copy solution for open systems servers (such as xSeries) as well as for zSeries servers. PPRC V2 was recently announced, and it provides for cascading functions. PPRC is discussed more fully in 6.2, “Peer-to-Peer Remote Copy (PPRC)” on page 63.

Note: XRC is only available for the z/OS and OS/390® environments, and not for Linux on zSeries or open systems.

# Point-in-time Copy function

Users still need to take backups to protect data from logical errors and disasters. For all environments, taking backups of user data traditionally takes a considerable amount of time. Usually, backups are taken outside of prime shift because of their duration and the consequent impact to normal operations. Databases must be closed to create consistency and data integrity, and online systems are normally shut down.

With the ESS Model 800, the backup time has been reduced to a minimal amount of time when using the FlashCopy® function. FlashCopy creates an instant point-in-time copy of data, and makes it possible to access both the source and target volumes immediately, thus allowing the applications to resume with minimal disruption. FlashCopy V2 was recently announced, which provides for multiple relationship and incremental FlashCopy functions. FlashCopy is discussed more fully in 6.4, “FlashCopy” on page 68.

Note: The IBM TotalStorage Enterprise Server Model 800 also provides a point-in-time copy function called Concurrent Copy, but this function is only available for the z/OS and OS/390 operating systems and not for Linux.

# Standby capacity on demand

To make the ESS Model 800 more scalable, and more able to accommodate dynamic and unpredictable workload requirements, the Standby Capacity on Demand feature has been announced. When your storage requirements increase, you can activate the additional capacity without any intervention from IBM, and without any interruptions to your work. When the standby capacity is activated, the ESS automatically reports the increase in capacity usage. Capacity on demand helps control costs while avoiding delays in acquiring storage that can result when the timing of capacity growth cannot be accurately forecasted.

# Storage Area Network (SAN)

The SAN strategy is to connect any server to any storage as shown in Figure 4-6 on page 44. As SANs migrate to 2 Gb technology, storage subsystems must exploit this more powerful bandwidth. Keeping pace with the evolution of SAN technology, the Enterprise Storage Server Model 800 is introducing new 2 Gb Fibre Channel/FICON host adapters for native server connectivity and SAN integration. These new 2 Gb Fibre Channel/FICON host adapters, which double the bandwidth and instantaneous data rate of the previous adapters available with the F Model, have one port with an LC connector for full-duplex data transfer over long-wave or short-wave fiber links. These adapters support the SCSI-FCP (Fibre Channel Protocol) and the FICON upper-level protocols. Each Fibre Channel port can be shared by multiple heterogeneous hosts and HBAs, potentially reducing the number of ports needed. LUN masking is included to support SAN security.