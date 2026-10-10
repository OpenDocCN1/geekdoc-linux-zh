| Command | Version Number | Not Used | AFI | Route Tag | Entry Address | Subnet Mask | Next Hop | Metric |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |

**Figure 6.22** RIP version 2 format.

+   12 Appletalk
+   13 Decnet IV
+   14 Banyan Vines

+   *   **Route Tag.** Specifies whether the route is internal or external.
+   *   **Entry Address.** IP address for the entry.
+   *   **Subnet Mask.** Subnet mask for the entry.
+   *   **Next Hop.** IP address of next hop router.
+   *   **Metric.** Lists the number of hops to destination.

# *Interior Gateway Routing Protocotl*

Cisco developed the Interior Gateway Protocotl (IGRP) for routing within an autonomous system, acting as a distance-vector interior gateway protocol. Merging both distance-vector and link-state technologies into one protocol, Cisco later developed the Enhanced Interior Gateway Protocol (EIGRP). The IGRP Packet format is shown in Figure 6.23; the Enhanced version (EIGRP) is shown in Figure 6.24. The format fields are defined as follows:

+   *   **Version Number.** Specifies the current protocol version.
+   *   **Operation Code (OC) Command.** Specifies whether the packet is a request or an update.

| Version Number | OC Command | Not Used | AS | AS Nets | Checksum |
| --- | --- | --- | --- | --- | --- |

**Figure 6.23** IGRP format.

| Version Number | OC Command | Checksum | AS Subnets | AS Nets | AS |
| --- | --- | --- | --- | --- | --- |

**Figure 6.24** EIGRP format.

| RN | ID Length | NID | Not Used | Start Range 1 | D | End Range 1 |
| --- | --- | --- | --- | --- | --- | --- |

**Figure 6.25** RTMP format.

**Autonomous System (AS).** Lists the AS number.

**AS Subnets.** Indicates the subnetworks outside of the current autonomous system.

**AS Nets.** Indicates the number and networks outside of the current autonomous system.

**Checksum.** Gives the standard UDP algorithm.

# *Appletalk Routing Table Maintenance Protocotl*