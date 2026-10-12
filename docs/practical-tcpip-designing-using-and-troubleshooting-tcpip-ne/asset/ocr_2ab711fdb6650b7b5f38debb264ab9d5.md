# **Table A16.1 Commonly used ethereal protocol names**

| Protocol | Description |
| :--- | :--- |
| arp | ARP |
| esp | Encapsulated Security Payload (VPN) |
| eth | Ethernet |
| frame | a “pseudo-protocol” to allow you to reference packet numbers and capture times. Of course these are not included in Ethernet packets but are stored with the packets in the capture file |
| ftp | FTP |
| http | HTTP |
| icmp | ICMP messages |
| ldap | LDAP |
| lpd | LPD printing |
| lanman | LAN Manager (Microsoft Windows Networking) |
| browser | network browsing (Microsoft Windows Networking) |
| netlogon | Network Logon (Microsoft Windows Networking) |
| netbios | NetBIOS (Microsoft Windows Networking) |
| nbns | NetBIOS name service (Microsoft Windows Networking) |
| nbss | NetBIOS session service (Microsoft Windows Networking) |
| nfs | Network File System |
| telnet | telnet |

# **Table A16.2 Commonly used ethereal field names**

| Field | Description |
| :--- | :--- |
| esp.spi | Security Parameter Index (VPN, Module 27.3) |
| eth.addr | MAC address (Ethernet) source or destination |
| eth.dst | destination MAC address (Ethernet) |
| eth.src | source MAC address (Ethernet) |
| eth.len | Ethernet packet length |
| eth.type | packet type (0800 = IP, 0806 = ARP) (Module 2.4) |
| frame.number | the frame number (packet number) in the packet list |
| icmp.type | ICMP message type (3 = destination unreachable, 11 = TTL exceeded, 8 = ping/echo request, 0 = ping/echo reply) |
| ip.addr | IP address, source or destination |
| ip.dst | IP destination address |
| ip.src | IP source address |
| ip.proto | IP protocol number (see Appendix 18) |
| tcp.dstport | TCP destination port |
| tcp.srcport | TCP source port |
| tcp.port | TCP port, source, or destination |
| udp.dstport | UDP destination port |
| udp.srcport | UDP source port |
| udp.port | UDP port, source, or destination |