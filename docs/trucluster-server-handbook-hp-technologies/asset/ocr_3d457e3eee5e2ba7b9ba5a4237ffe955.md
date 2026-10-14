device through the DRD server only). This is similar to how the Distributed Raw Disk (the other DRD) component of the TruCluster Production Server product functions¹.

The direct approach is accomplished using devices that are Direct Access I/O (DAIO) capable. The DAIO implementation grew out of the Multi-Node Simultaneous Access (MUNSA)² work that was done for TruCluster Production Server version 1.5.

# 15.1.2.1 Direct Access I/O (DAIO) Device

A device can be served by more than one DRD if the device is Direct Access I/O capable. What determines whether or not a device is DAIO capable?

+   - The device must have hardware bad block replacement enabled.
+   - The device must support tagged queuing to allow command ordering from a host.
+   - The device must support simultaneous access from multiple initiators.

All disk devices supported by TruCluster Server versions 5.0A, 5.1, and 5.1A are DAIO capable.

Figure 15-3 illustrates how a DAIO device is accessed in a four-member cluster. In the figure you can see that every member in the cluster can directly access the disk. The captions for each member show a slightly modified view that you would get if you ran the drdmgr (8) command on each member. Since every member in the cluster has a physical connection to the bus where the disk is located, the "number of servers" attribute has a value of four. The servers are listed in the "server name" fields. The fact that all four members' "server state" is "Server" indicates that all four members can actively access this disk. Valid server states are: "Server" and "Not Server".

Although there are four active servers for this device, each member will access the disk via one server at a time. The server that the member is currently using to access the device is indicated by the "access member name". By default, if the member is also a server, its "access member name" will always be itself.

In Figure 15-3, every member has direct access because they are physically connected to the bus where the device is attached and the device supports DAIO (as indicated by the "device type" field). As of this writing, there are four valid device types that you will see in the output of the drdmgr command: "Direct Access IO Disk" (indicated as DAIO in the figure), "Served Disk", "Served Tape", and "Served Changer".

A device can be DAIO and yet have members in the cluster that cannot directly access the device. Although the device is capable of having more than one server, due to physical connectivity the device may have only one server. Figure 15-4 illustrates a DAIO device on a private bus. The DRD

> ¹ See chapter 2 for more information on Distributed Raw Disk and TruCluster Production Server.
> ² MUNSA was not part of the shipping product. It was a special patch created for a customer.