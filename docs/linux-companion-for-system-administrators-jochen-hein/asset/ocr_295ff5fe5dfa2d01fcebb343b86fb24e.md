accessing Windows shares. Shared printers can be addressed by means of the sambient program from the samba package.

For communication with Apple Macintosh computers, AppleTalk protocol is employed. Here too, there is with an implementation under Linux. With this, Linux is a truly open and communicative operating system is also due to the fact that practically the whole source code is available and any interested party can make changes and adaptations to it.

# 19.1 LINUX as a NetWare client and server

Novell NetWare is very popular in local PC networks. The implementation is stable and faster than the TCP/IP protocols. Several years ago, when PCs were much less powerful, this was often the only reason of networking. Today, also also because of the Internet and intranet strategies, TCP/IP is gaining a growing importance - even NetWare migrates towards TCP/IP. IPX is used as the lowest protocol layer. This protocol is documented and has been implemented in the Linux kernel for some time. Linux can also be used as an IPX router, and NetWare services can be accessed in the DOSemu.

NetWare services, that are file and print services, are however based on the NetWare Core Protocol (NCP) which is based on IPX, but was not officially documented by Novell. This documentation is now (at least partly) available, so that Linux can be employed in NetWare networks both as a client and as a server.

First of all, the IPX protocol must be compiled into the kernel. This implementation has been carried out by, among others, Caldera. a company initially financed by former Novell CEO Ray Noorda. After a reboot, the kernel signals the presence of this protocol with a message such as:

> Indiana University Computer Society IPX 0.34 for NET3... IPX Portions Copyright (c) 1995 Caldera, Inc.

Subsequently, similarly to TCP/IP networks, the interface must be configured. Currently, this is still done by means of a separate program. These functions can in future be integrated into the ifconfig program. Configuration of the interface can be carried out either automatically or manually. With the command ipx_configure --auto_primary=on -auto_interface= you will automatically create a primary IPX interface when an IPX packet arrives.

Automatic recognition is only possible if you want to operate LINUX only as a client in the network. Otherwise, you will need an internal IPX network