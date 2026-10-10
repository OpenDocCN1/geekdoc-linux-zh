ality continues to increase to a point where you are working with files that can be stored on any system on the network, and your access to these files is transparent to you with the Network File System (NFS).

Let's take a look at some of the basics of UNIX networking.

# # An Overview of IEEE802.3, TCP/IP

In order to understand how the networking on your UNIX system works, you first need to understand the components of your network that exist on your UNIX system. Seven layers of network functionality exist on your UNIX system, as shown in Figure 13-2. I cover the bottom four layers at a cursory level so that you can see how each plays a part in the operation of your network and, therefore, be more informed when you configure and troubleshoot networking on your UNIX system. The top layers are the ones that most UNIX system administrators spend time working with because those layers are closest to the functionality to which you can relate. The bottom layers are, however, also important to understand at some level, so that you can perform any configuration necessary to improve the network performance of your system, which has a major impact on the overall performance of your system.

| Layer Number | Layer Name | Data Form | Comments |
| :--- | :--- | :--- | :--- |
| 7 | Application | | User applications here. |
| 6 | Presentation | | Applications prepared. |
| 5 | Session | | Applications prepared. |
| 4 | Transport | Packet | Port-to-port transportation handled by TCP. |
| 3 | Network | Datagram | Internet Protocol (IP) handles routing by going directly to either the destination or default router. |
| 2 | Link | Frame | Data encapsulated in Ethernet or IEEE 802.3 with source and destination addresses. |