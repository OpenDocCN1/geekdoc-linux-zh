A server's boot sector and OS files can't be infected unless the server is started from an infected disk. As a result, Eric has developed the habit of scanning all disks before inserting them in the server and has modified the server's CMOS to prevent it from starting from a disk that might have been left in the drive inadvertently.

# Defense Against Denial-of-Service Attacks

Although denial-of-service attacks don't usually damage or steal a company's data directly, they can result in high costs by bogging down the organization's Web services, causing lost customer sales and reducing user productivity. Denial-of-service attacks are usually caused by flooding a server with packets or sending oversized packets to a service, causing it to crash. A correctly configured firewall and software designed for Net Services security are the best defenses against denial-of-service attacks. Table 11-2 describes common denial-of-service attacks that Luke listed in his UAS Internet security proposal.

| Table 11-2 Common denial-of-service attacks | | |
| :--- | :--- | :--- |
| **Type of Attack** | **Description** | |
| Ping of death | The PING command is modified to send Internet Control Message Protocol (ICMP) Echo packets longer than the 64 KB maximum defined in the TCP/IP RFC 791 standard. The extra bytes in the packet can cause unprotected TCP/IP software to overflow the buffer space, resulting in computer hang-ups or crashes. | |
| Teardrop attack | The teardrop attack intentionally overlaps packet fragments, causing errors in fragment reassembly that can result in packets being resent repeatedly and flooding the server. | |
| Land attack | The land attack sends packets with the same source and destination IP addresses, thereby flooding the service with an endless loop of packets being sent to the server. | |
| SYN packet flooding | TCP connections require the following three-way handshake between the server and the client:
1. The client sends a packet in which the SYN flag is set in the TCP header.
2. The server sends a SYN/ACK (acknowledgment) packet back to the client.
3. The client sends an ACK packet so that data transmission can begin.
A TCP SYN denial-of-service condition is caused when the client fails to send the last ACK packet and intentionally sends successive TCP connection requests to the server, filling up the server's buffer. After the server's buffer is full, other client requests are rejected, resulting in a denial-of-service condition. | |
| Oversized UDP packets | Like the ping of death, sending oversized UDP packets can result in buffer overflows that cause the server to hang or crash. | |
| Smurf | Smurf attacks use the ICMP Echo in response to PING broadcasts to flood the server. | |

The ping of death is perhaps one of the best-known denial-of-service attacks. Normally, the Packet Internet Gopher (PING) application is used as a diagnostic utility on TCP/IP networks to send Echo packets to selected hosts and receive responses if the network and host are operational. By default, Echo packets contain only 64 bytes of data, but the RFC standard allows up to 64 KB. The ping of death occurs when a PING command is sent to an IP host with more than 64 KB of data. Some older software can't handle these large Echo packets, which can cause the TCP/IP stack to overflow, thereby slowing down or crashing the server. It's the OS software vendor's responsibility to ensure that its TCP/IP implementation can handle oversized Echo packets.