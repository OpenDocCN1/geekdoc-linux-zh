
TCP/IP networks are configured and managed with a set of utilities: ifconfig, route, and netstat. The ifconfig utility operates from your root user desktop and enables you to configure your network interfaces fully, adding new ones and modifying others. The ifconfig and route utilities are lower-level programs that require more specific knowledge of your network to use effectively. The netstat utility provides you with information about the status of your network connections. Ethereal is a network protocol analyzer that lets you capture packets as they are transmitted across your network, selecting those you want to check.

| Category | Protocol | Description |
|---|---|---|
| Transport | TCP | Transmission Control Protocol; places systems in direct communication |
| Transport | UDP | User Datagram Protocol |
| Transport | IP | Internet Protocol; transmits data |
| Transport | ICMP | Internet Control Message Protocol; status messages for IP |
| Routing | RIP | Routing Information Protocol; determines routing |
| Routing | OSPF | Open Shortest Path First; determines routing |
| Network Addresses | ARP | Address Resolution Protocol; determines unique IP address of systems |
| Network Addresses | DNS | Domain Name Service; translates hostnames into IP addresses |
| Network Addresses | RARP | Reverse Address Resolution Protocol; determines addresses of systems |
| User Services | FTP | File Transfer Protocol; transmits files from one system to another using TCP |
| User Services | TFTP | Trivial File Transfer Protocol; transfers files using UDP |
| User Services | Telnet | Remote login to another system on the network |
| User Services | SMTP | Simple Mail Transfer Protocol; transfers e-mail between systems |
| User Services | RPC | Remote Procedure Call; allows programs on remote systems to communicate |
| Gateway | EGP | Exterior Gateway Protocol; provides routing for external networks |
| Gateway | GGP | Gateway-to-Gateway Protocol; provides routing between Internet gateways |
| Gateway | IGP | Interior Gateway Protocol; provides routing for internal networks |
| Network Services | NFS | Network File System; allows mounting of file systems on remote machines |
| Network Services | NIS | Network Information Service; maintains user accounts across a network |
| Network Services | BOOTP | Boot Protocol; starts system using boot information on server for network |
| Network Services | SNMP | Simple Network Management Protocol; provides status messages on TCP/IP configuration |
| Network Services | DHCP | Dynamic Host Configuration Protocol; automatically provides network configuration information to host systems |

## IPv4 and IPv6

Traditionally, a TCP/IP address is organized into four segments, consisting of numbers separated by periods. This is called the IP address. The IP address actually represents a 32-bit integer whose binary values identify the network and host. This form of IP addressing adheres to Internet Protocol, version 4, also known as IPv4. IPv4, the kind of IP addressing described here, is still in wide use.

Currently, a new version of the IP protocol called Internet Protocol, version 6 (IPv6) is gradually replacing the older IPv4 version. IPv6 expands the number of possible IP addresses by using 128 bits. It is fully compatible with systems still using IPv4. IPv6 addresses are represented differently, using a set of eight 16-bit segments, each separated from the next by a colon. Each segment is represented by a hexadecimal number. A sample address would be:

```
FEC0:0:0:0:800:BA98:7654:3210
```

Advantages for IPv6 include the following:

- Features simplified headers that allow for faster processing.
- Provides support for encryption and authentication along with Virtual Private Networks (VPN) using the integrated IPSEC protocol.
- Extends the address space to cover 2 to the power of 128 possible hosts (billions of billions). This extends far beyond the 4.2 billion supported by IPv4.
- Supports stateless autoconfiguration of addresses for hosts, bypassing the need for DHCP to configure such addresses. Addresses can be generated directly using the MAC (Media Access Control) hardware address of an interface.
- Supports Quality of Service (QoS) operations, providing sufficient response times for services like multimedia and telecom tasks.
- Multicast capabilities built into the protocol, providing direct support for multimedia tasks. Multicast addressing also provides that same function as IPv4 broadcast addressing.
- More robust transmissions can be insured with anycast addressing, where packets can be directed to an anycast group of systems, only one of which needs to receive them. Multiple DNS servers supporting a given network could be designated as an anycast group, of which only one DNS server needs to receive the transmission, providing greater likelihood that the transmissions will go through.
- Better access for mobile nodes, like PDAs, notebooks, and phones.

## TCP/IP Network Addresses

As noted previously, the traditional IPv4 TCP/IP address is organized into four segments, consisting of numbers separated by periods. This kind of address is still in wide use and is what people commonly refer to as an IP address. Part of an IP address is used for the network address, and the other part is used to identify a particular interface on a host in that network. You should realize that IP addresses are assigned to interfaces—such as Ethernet cards or modems—and not to the host computer. Usually a computer has only one interface and is
