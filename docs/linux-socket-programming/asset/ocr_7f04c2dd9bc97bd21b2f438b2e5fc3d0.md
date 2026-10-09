# Table A.2, Protocol Values for the *type* Parameter in `socket( )` Call

| Protocol Type | Description |
| :--- | :--- |
| **SOCK_STREAM** | (TCP) Reliable, two-way communication in a stream. You can use this kind of socket in higher-level I/O function calls that involve the `FILE*` type. This protocol offers you a virtual connection to the network using ports and a dedicated client channel. After connection, the `accept( )` call returns a new socket descriptor specifically for the new client. |
| **SOCK_DGRAM** | (UDP) Unreliable connectionless communication. Each message is independent and can be lost during transmission. This protocol virtualizes the network with ports and allows you to send and receive messages from many peers without reconnection. |
| **SOCK_RAW** | (IP) Accesses the internal network interfaces and fields. If you want to create ICMP messages, you need to create a raw socket. Root access only. |
| **SOCK_RDM** | (RDM—Reliably Delivered Messages) Makes sure that each packet arrives safely to the destination, but does not guarantee correct packet order. (Not yet implemented in Linux and other UNIX operating systems.) |
| **SOCK_SEQPACKET** | Sequenced, reliable, connection-based datagrams of fixed length. (Not yet implemented in Linux.) |
| **SOCK_PACKET** | (Physical Layer) Places the socket in promiscuous mode (if available) where it will receive any and all packets on the network. This is a Linux-only tool. Root-access only. (Deprecated—use PF_PACKET instead.) |

# Protocol Definitions

*Listing A.1* is an excerpt from the `/etc/protocols` file [RFC2292] on your distribution. It contains the common and standard protocol standards used in the network packet. Revising this file is *not* a good idea.

# *Example A.1. /etc/protocols File*

```
```
ip		0 IP		# internet protocol, pseudo number
icmp		1 ICMP		# internet control message protocol
igmp		2 IGMP		# Internet Group Management
ggp		3 GGP		# gateway-gateway protocol
ipencap	4 IP-ENCAP	# IP encapsulated in IP
st		5 ST		# ST datagram mode
tcp		6 TCP		# transmission control protocol
egp		8 EGP		# exterior gateway protocol
pup		12 PUP		# PARC universal packet protocol
udp		17 UDP		# user datagram protocol
hmp		20 HMP		# host monitoring protocol
xns-idp	22 XNS-IDP	# Xerox NS IDP
rdp		27 RDP		# "reliable datagram" protocol
iso-tp4	29 ISO-TP4	# ISO Transport Protocol class 4
xtp		36 XTP		# Xpress Tranfer Protocol
ddp		37 DDP		# Datagram Delivery Protocol
idpr-cmtp	39 IDPR-CMTP	# IDPR Control Message Transport
rsrp		73 RSRP		# Radio Shortest Path First
vmtp		81 VMTP		# Versatile Message Transport
ospf		89 OSPFIGP	# Open Shortest Path First IGP
ipip		94 IPIP		# Yet Another IP encapsulation
encap		98 ENCAP		# Yet Another IP encapsulation
```
```

# Standard Internet Port Assignments (First 100 Ports)

*Listing A.2* shows the standard ports (up to port #100) defined in the `/etc/services` file. You can change many of these to suit your needs, but be sure to notify the clients if you do so.