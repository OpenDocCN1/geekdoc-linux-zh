# 13.1 The Internet Protocol Suite 225

be forwarded because routing information is missing or faulty. Section 14.4 allows
with ICMP and its implementation in Linux.

The Internet Group Management Protocol (IGMP) is responsible for managing
micast groups in local area networks. Multicast is responsible for efficient sending
data to a specific group of computers. IGMP allows the computers of a LAN to
inorm its router that they want to receive data for a certain group in the future.
Chapter 17 discusses multicast in the Internet.

The Transmission Control Protocol (TCP) is a reliable, connection-oriented and
byte-stream-oriented transport-layer protocol. TCP is primarily responsible for
providing a secured data transport between two applications over the unreliable
service of the IP protocol TCP is the most frequently used transport protocol in
t Internet. It has a large functionality, and so its implementation is extensive.
Chapter 24 discusses the TCP.

The Data Datagram Protocol (UDP) is a very simple transport protocol, providing
connectionless and unreliable transport of data packets between applications in the
Internet. In this context, unreliable does not mean that the data could cor-
rupted at the destination computer. It means that UDP does not offer any protocol
mechanisms to guarantee that the data will arrive at all. When
data arrives at the destination computer, it can only be checked for correctness.

As compared with TCP, UDP has the benefit that it has very little functionality
 so can easily be extended. Many applications that normally transmit only
small amounts of data (e.g., client/server applications) use UDP as their per-
ferred protocol. Establishing a connection and reliable data transmis-
sion would be more costly than the retransmission of faulty or missing data.

The application layer accommodates various standardized application protocols,
which form the basis of a large number of applications:

+   The HyperText Transfer Protocol (HTTP) is currently the protocol most
frequently used in the Internet application layer. It allows you to exchange
data in the World Wide Web—say, by loading sites into your Web browser
(Netscape, Mozilla, Lynx, etc.). The unprecedented success of the World Wide
Web led to the enormous proliferation of the Internet and its
revolutionary growth.

+   TELNET is the protocol for virtual machines. It is used to access a computer
connected to the network in the form of a terminal session. Its unsecured
transmission of passwords and data has caused TELNET to be increasingly
replaced by the SSH (Secure Socket Shell) protocol.

+   The File Transfer Protocol (FTP) is used to transport files from a local
computer to another computer and vice versa. Like TELNET, its most
important drawback is that passwords are transmitted in cleartext. FTP has
increasingly been replaced by Secure Copy (SCP).

+   The Simple Mail Transfer Protocol (SMTP) is the protocol used to exchange
eelectronic mail (e-mail) in the Internet.