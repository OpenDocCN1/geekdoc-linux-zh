# Understanding VLAN

VLAN is an acronym for Virtual Local Area Network (normally referred to Virtual LAN). It refers to a switched network that is segmented logically using a project team, application or function. The logical segmentation is done without consideration of users' physical locations. VLANs are more or less same as physical LANs. The only difference is that VLANs allow end stations to be grouped regardless of whether they are on the same physical segment or not. A VLAN can accommodate any form of switch module port. Multicast, broadcast and unicast data packets can be forwarded and flooded to end stations only in a given VLAN. Each VLAN is taken as a logical network. Packets destined for stations outside of a VLAN must be forwarded through a router to reach its destination. Notably, a VLAN can be associated with an IP sub-nets.

# Supported VLANs

Conventionally, we identify VLANs with a number ranging from 1 to 4094.
The following must be noted:

+   - 1002-1005 VLAN IDs are reserved for FDDI and Token Ring VLANs
+   - VLAN IDs > 1005 are not found in the VLAN database since they are extended range.
+   - Switch module supports extended-range and normal range VLANs (1005).
+   - Number of configured features, SVIs and routed ports affects functioning of the switch module hardware.

# VLAN Configuration Guidelines

It is important to understand the following facts:

+   - 1005 VLANs are supported on the switch module.
+   - Numbers between 1 and 1001 are used to identify normal-range VLANs.
+   - 1002 -1005 are reserved for FDDI and Token Ring VLANs.
+   - Switch module has no FDDI and Token Ring support.
+   - 1-1005 VLAN IDs are normally stored in the VLAN database as well as the file containing the switch module configuration information.
+   - 1006-4094 (extended-range) VLAN IDs are limited to private LAN, RSPAN VLAN, MTU, and UNI-ENI VLANs. These VLAN IDs are not saved in the VLAN database.

The following steps will help you create or modify a VLAN:

+   1. Use the [configure terminal] command to enter the global configuration mode.
+   2. Enter the [vlan <vlan-id>] to enter VLAN configuration mode.