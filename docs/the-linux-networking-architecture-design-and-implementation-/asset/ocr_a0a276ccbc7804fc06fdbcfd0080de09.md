# ISO/OSI reference model

# 3.1 Layer-based Communication Models

| ISO/OSI reference model | Internet reference model |
| --- | --- |
| Application | Application (HTTP, SMTP, SSH) |
| Presentation | |
| Session | |
| Transport | Transport (TCP/UDP) |
| Network | Internet (IPv4/v6) |
| Data Link | Data link (802.x, PPP, SLIP) |

FIGURE 3-3 Comparing the ISO/OSI reference model and the TCP/IP reference model.

computer systems have changed from large mainframe systems to private workstations. As a result, researchers who developed TCP/IP invented a new layering model. This section describes the new layering model briefly.

The TCP/IP layering model, which is also called Internet Reference Model, contains the following layers (shown in Figure 3-3):

+   * Application layer: The application layer combines all application-specific tasks (i.e., the properties of layers 5 to 7 of the ISO/OSI model). The protocols of the application layer include Telnet (for virtual terminals), FTP (file transfer), and SMTP (to transmit e-mail). More protocols include DNS (Domain Name System) and HTTP (Hypertext Transfer Protocol).

+   * Transport layer: In the ISO/OSI model, the transport layer of the TCP/IP reference model allows end-system applications to communicate. The TCP/IP reference model defines two basic protocols for this purpose: The Transmission Control Protocol (TCP) and the User Datagram Protocol (UDP). TCP is a reliable connection-oriented protocol and can transmit a stream without errors over the network. UDP is unreliable and connection, but is preferred over the more complex TCP in many situations (e.g., to transmit multimedia data).

+   * Internet layer: The Internet layer of the TCP/IP reference model defines the Internet Protocol (IP), including two auxiliary protocols, the Internet Control Message Protocol (ICMP) and the Internet Group Management Protocol (IGMP). The main purpose of the Internet layer is to forward packets from the sender to the receiver over the network, where routing of packets plays an important role. The Internet Control Message Protocol (ICMP) is an integral part of each implementation: it serves to transmit diagnostics and error information for the Internet Protocol. The Internet Group Management Protocol (IGMP) is used to manage communication groups.

+   * Interface layer: This layer combines the two lower layers of the ISO/OSI reference model. It handles network adapters and their drivers, which are used to exchange data packets in a specific maximum length over a local area network (Ethernet, Token Ring, etc.) or over a wide area network (ISDN, ATM).