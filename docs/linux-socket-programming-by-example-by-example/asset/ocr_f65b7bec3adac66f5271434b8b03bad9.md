# Other Linux-Supported Protocols

| Domain | Socket Type | Description/Notes |
| :--- | :--- | :--- |
| PF_AX25 | SOCK_DGRAM | Datagram service for the amateur radio protocol AX.25. This provides for unreliable connectionless communications. |
| PF_APPLETALK | SOCK_STREAM | Stream I/O services for the AppleTalk-connected sockets. This connection-oriented service is reliable and data sequence is preserved. |
| PF_APPLETALK | SOCK_DGRAM | This has been provided in Linux as an extension. See kernel documentation or sources for more details. |
| PF_ECONET | SOCK_DGRAM | An implementation of the Acorn Econet and AUN protocols. |
| PF_IPX | SOCK_STREAM | IPX protocol, stream socket. |
| PF_IPX | SOCK_DGRAM | IPX protocol, datagram socket. |
| PF_IPX | SOCK_SETPACKET | IPX protocol, sequential packet socket. |
| PF_IRDA | SOCK_STREAM | IRDA subsystem support, using a stream socket (infrared communications). |
| PF_IRDA | SOCK_SETPACKET | IRDA subsystem support, using a stream socket that preserves message boundaries (infrared communications). |
| PF_NETROM | SOCK_SETPACKET | Amateur radio NetROM protocol. |
| PF_ROSE | SOCK_SETPACKET | Amateur radio X.25 PLP 1 protocol. |

# Researching Other Protocols

Many of the protocols listed in Table 4.3 are still undergoing development. Consequently, documentation is sparse in some areas. Nevertheless, here are some ideas regarding where you can scare up more information:

+   - Linux HOWTO and MINI-HOWTO documents.
+   - Linux FAQ documents.
+   - The /usr/src/linux/Documentation/networking Linux source directory. If you use a different source directory, then substitute that for the directory /usr/src/linux.
+   - The Linux source directory /usr/src/linux/net. There, you will find other subdirectories of source code, many of which have to do with specific protocols.

There are many HOWTO and MINI-HOWTO documents on the Internet that you can search out. FAQ is short for Frequently Asked Questions. Sometimes these files can be very helpful.