# 50 Chapter 3 The Architecture of Communication Systems

Data link layer: This layer specifies how data should be transmitted between two stations directly connected over a medium. The sending system organizes the data in frames and transmits them back to back. If errors occur, then the data link layer is responsible for detecting such errors and retransmitting the data frames. Moreover, the data flow between the two systems should be regulated so that the receiver does not get overloaded (flow control). Examples of data-link layer protocols are HDLC (High-level Data Link Control), SLIP (Serial Line IP), and PPP (Point-to-Point Protocol); the latter two offer the described functions to only a limited extent.

In local networks, the data link layer often assumes the task to regulate access to a shared medium. In such cases, the data link layer is divided into the Medium Access Control (MAC) layer and the Logical Link Control (LLC) layer.

Network layer: The network layer is responsible for establishing connectivity between all systems of a telecommunication network. For this reason, the network layer deals with switching and forwarding of data units (e.g., routing, adapting data units to the admissible size of the respective data link layer (fragmenting), or ensuring various service qualities). Within the scope of this book, we will mainly discuss the Internet protocols Versions 4 and 6.

Transport layer: The transport layer regulates the transport of data between applications (i.e., between the sender and the receiver application). Among others, it is responsible for addressing applications, for controlling the data flow between the two systems, and for securing both the correctness and the order of data.

Session layer: The session handles the structured exchange of messages over transport links. For example, it can control within a system whether the transfer of data should be concurrently in both directions or only one of the communicating partners should have the right to transmit. In the latter case, the session layer manages the right to transmit.

Presentation layer: The presentation layer regulates the presentation of data in a format independent of the communicating systems. Many operating systems use different forms of representation for characters (e.g., ASCII, Unicode), numbers (big-endian, little-endian). To ensure that this data can be exchanged between the systems involved, the representation layer transmits it in a standardized form (e.g. by using Abstract Syntax Notation (ASN.1) or Basic Encoding Rules (BER).

Application layer: This layer uses specific protocols for different applications, using the lower-layers to fulfill their tasks—for example, the application layer protocols for electronic mail, file transfer, and remote procedure call.

# 3.1.2 The TCP/IP Reference Model

The naming convention for the Internet reference model is based on the most important Internet protocols—the Transmission Control Protocol (TCP) and the Internet Protocol (IP). The 7-layer ISO/OSI reference model described earlier was devised before internetworking was invented. Furthermore, the 7-layer reference model devotes an entire layer to session protocols, which become much less important as