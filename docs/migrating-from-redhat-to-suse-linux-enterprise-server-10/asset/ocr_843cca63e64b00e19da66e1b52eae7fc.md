# **Objective 1**

# iSCSI Background

SCSI commands are used to enable systems to communicate with I/O devices, especially storage devices. The Internet Small Computer Systems Interface implements the regular SCSI commands over IP.

With iSCSI, the operating system (iSCSI initiator) does not send the SCSI command directly to a device, but to another system connected via the network (iSCSI target); this system will then redirect the SCSI commands to the actual storage device—for instance a partition, a logical volume or a file.

This is basically a client/server connection between iSCSI initiator (client) and iSCSI target (server). However, unlike usual client/server connections, usually only one client may connect to the server. The iSCSI protocol is standardized in RFC3720.

With iSCSI it is possible to connect to remote storage, which can be a disk, a logical volume or a file, and it will appear to the system as a local disk. This is also known as SAN. The advantage of iSCSI in comparison to other SAN solutions is primarily in the area of cost. Common SAN solutions use rather expensive FC (fibre channel) hardware, whereas iSCSI can use the already existing ethernet network. Furthermore, many SAN solutions also provide an iSCSI interface.

Considering the amount of data transferred over the network it is important that enough bandwidth is available, for instance Gigabit Ethernet. It often makes sense to set up a dedicated network for the iSCSI connections.

The remote devices are available on Linux as a regular SCSI (\*/dev/sdX\*) device and should be mounted with the option `ntdev`. You can configure the iSCSI targets to require a username and password upon connection from an iSCSI initiator.