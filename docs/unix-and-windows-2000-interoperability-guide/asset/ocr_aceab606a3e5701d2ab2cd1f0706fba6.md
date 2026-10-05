# 13.1.1 An NAS Example

To illustrate the NAS concept, let's look at the EMC Celerra file server. There are two components to the Celerra: the file server itself and the storage. The storage consists of a disk array called the Symmetric, either contained in the same cabinet as the file server or existing in a separate cabinet. The file server connects to the disk array either over a SCSI or Fibre Channel connection. It connects to the network via 10/100BaseT Ethernet, Gigabit Ethernet, Fiber Distributed Data Interface (FDDI), or Asynchronous Transfer Mode (ATM). Clients connect to the file server over the network via NFS or CIFS. Figure 13–1 illustrates these components.

![](bbox=[0.118, 0.329, 0.803, 0.775])

Figure 13–1 Components of Network-Attached Storage. This diagram shows the file server connected to a separate disk array. There are other file servers that share their cabinets with the disks, creating a single enclosure.

In addition to CIFS, the Celerra file server supports both version 2 and version 3 of NFS and both UDP and TCP as NFS transports. It also supports FTP and WebNFS, which lets you access NFS file systems using Web browsers, Java applets, and the Internet.