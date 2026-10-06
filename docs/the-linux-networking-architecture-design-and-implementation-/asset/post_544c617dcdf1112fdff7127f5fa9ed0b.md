
# 14.3 IP Options 253

| 10000010 | 00001011 | Security |
|---|---|---|
| Compartments | | Restrictions |
| Transmission Control Code | | |

The Security option is used primarily in military networks; it comprises a total of 11 bytes. The Security option allows end systems to send security parameters or define own (controllable) groups of communication partners, which want to exchange IP packets in "isolation" from all other traffic. The two-byte Security field can be used to state 16 security levels for an IP packet; of these the original RFC 791 defines eight levels, including Unclassified, Confidential, Restricted, Secret or Top Secret. The other security levels are reserved for future use. As the One in the first bit (corresponding to the Copy Flag) of this packet option already states, this packet option has to be set in each fragment, if IP packets are fragmented.

These fields are primarily specified by the Defense Intelligence Agency. For this reason, the current implementation in Linux does not support the Security option.

# Loose Source Routing
Bit sequence:

| 10000011 | Length | Pointer | Route Data |

This option is used to specify all routers an IP packet has to visit on its way across the network. In addition, it accepts data about the packet's path. The third byte includes a pointer to the address of the next router that the packet has to pass. This pointer is relative to this option—the smallest possible value is 0. If the pointer points to a byte not belonging to this option according to the length byte, then the packet can be sent over an arbitrary path to the actual destination address. In contrast, if the packet has reached the address specified in the destination field, yet the pointer still points to another valid address, then the destination field is overwritten with this address. The pointer is incremented by the length of an IP address, 4 bytes. The consequence of this placement strategy is that the protocol header of the IP packet maintains a constant length all the time. In contrast to the Record route packet option, addresses are defined exclusively by the sender; no addresses are entered by intermediate systems.

If the packet has to be fragmented, then this packet option has to be copied to each packet fragment, because the fragments are forwarded independently of one another, which means that they can reach the receiver over different paths across the Internet.

# Strict Source Routing
Bit sequence:

| 10001001 | Length | Pointer | Route Data |

The Strict Source Routing option differs in only one point from the Loose Source Routing option: the packet may pass exactly those routers specified in the Route Data list. If a packet arrives in a router not explicitly present in this list, then an ICMP message to be generated and returned to the sender. Section 14.4 describes the Internet Control Message Protocol (ICMP).

As with the previous option, if fragmentation is required, then the Strict Source Routing option has to be copied in each single fragment, which means that One is in the first position of this option.

# Record Route
Bit sequence:

| | Length | Pointer | Route Data |
| 0000111 | | | |

The Record Route option can be used to register the addresses of all intermediate systems an IP packet will pass on its way to the destination. The third byte includes a pointer to the field that is to the next address. The length of this option should never change; the sender specifies twice the available space, which is initially filled with zeros. These zeros are not treated as an End of Option List, because the length by Length, states the option's length. Each Internet node adds its address in a field specially provided for this purpose and increases the pointer by four [bytes] (corresponding to the length of an IP address). If no more space is available, then the IP packet is forwarded without storing the address. In this case, an ICMP message can be returned to the sender.

In contrast to the two previous packet options (i.e., Loose Source Routing and Strict Source Routing), this option appears only in the first fragment, if an IP packet has to be fragmented.

# Stream Identifier
Bit sequence:

| 10001000 | 00000010 | Stream ID |

This option enables the transport of SATNET Stream Identifiers across the Internet. The Stream Identifier packet option is always 4 bytes long and has to be copied to all fragments, if fragmentation is used. However, this option currently has no practical use, and we use it here for the sake of completeness.

# Internet Timestamp
Bit sequence:

| 01000100 | Length | Pointer | Counter | Flag |
| Address | Timestamp | | | |

The original RFC 791 includes the Internet Timestamp option as the only packet of class 2 (i.e., debugging or measurement options). This option can be used to store time stamps of selected or all network nodes. A 4-bit flag determines the data to be stored here, and it can take either of the following values:

- 0—The option stores time stamps only.
- 1—The option stores all time stamps and addresses.
- 2—A router completes its timestamp if its address is listed in this option.

Notice that the size of the Internet Timestamp option does not change, because the sender specifies it in the length field. For this reason, there is an additional (4-bit) Counter field, which includes the number of all routers for the time stamps of which there was no space in the data field. The maximum length of this option is 40 bytes. The third byte points to the next four or eight bytes to be filled. If fragmentation is required, this option appears in the first fragment, and so the Copy Flag is set to 0.

# 14.3.2 Configuration

Each Linux user can use the traceroute command to track an IP packet on its way across the Internet to the destination node. This might suggest that the Record Route option is used in this case. Actually, this is not so: traceroute uses another method for several reasons:

- Formerly, not all routers supported the Record Route option, which means that they wouldn't be available for use.
- Record Route is normally intended for one-way—the receiver has to return an echo of the IP packet to the sender. This means that the recorded addresses would be duplicated.
- The main reason is lack of space: a maximum of nine IP addresses fits into the list. Formerly, this might have been sufficient, but today the average number of intermediate systems for a connection across the Internet is much higher. For these reasons, traceroute uses the Internet Control Message Protocol (ICMP, see Section 14.4) and the Time-to-Live (TTL) field of the IP header, which stores the lifetime of the packet and increments the value at each step. The first packet gets a lifetime of one (i.e., the first Internet node returns an ICMP message as soon as it receives the packet), so that it can follow the path to the destination address. However, a trick has to be used if the packet is not delivered locally. Notice, however, this method only works because all IP packets from a sender normally take the same path through the receiver. When the first version of traceroute included this option, many system administrators found that it results in an excessive load on routers. Consequently, to use these packet options today, we need a corresponding patch. The following example uses Loose Source Routing:

```
# traceroute -g 129.13.92.254 rzstud1.rz.uni-karlruhe.de (129.13.197.1)
30 hops max
40 packets
1 rasc01.rz.uni-karlruhe.de (129.13.92.1) 20 ms 20 ms
2 r-ascend-netz.rz.uni-karlruhe.de (129.13.92.254) 20 ms 20 ms
3 rzstud1.rz.uni-karlruhe.de (129.13.197.1) 23 ms 22 ms 24 ms
```

Because the traceroute command, which is normally installed in Linux, does not let a user access the IP packet options, another way to use it is by the ping. Ping is intended to verify that a host is reachable. For this purpose, it continuously sends ICMP requests to the destination computer and expects a reply in the form of an ICMP message. Today, there are still ping implementations that allow you to use the packet options Source Routing and Internet Timestamp. For the same reasons as removed from most implementations, only the Record Route option remained. The following example shows how you can use ping with the Record Route option. The route is out after the first request.

```
# ping -R rzstud1.rz.uni-karlruhe.de
rzstud1.rz.uni-karlruhe.de (129.13.197.1): 56 data bytes
64 bytes from 129.13.197.1: icmp_seq=0 ttl=253 time=235.977 ms
RR: isdn216-10.rz.uni-karlruhe.de (129.13.216.100)
rzasc01.rz.uni-karlruhe.de (129.13.92.1)
129.13.197.62
rzstud1.rz.uni-karlruhe.de (129.13.197.1)
r-ascend-netz.rz.uni-karlruhe.de (129.13.92.254)
rzasc01.rz.uni-karlruhe.de (129.13.92.1)
isdn216-10.rz.uni-karlruhe.de (129.13.216.100)
64 bytes from 129.13.197.1: icmp_seq=1 ttl=253 time=47.171 ms (same route)
64 bytes from 129.13.197.1: icmp_seq=2 ttl=253 time=48.728 ms (same route)
---
rzstud1.rz.uni-karlruhe.de ping statistics --
9 packets transmitted, 9 packets received, 0% packet loss
round-trip min/avg/max = 45.100/70.5/235.97 ms
```

If the local computer has root rights, then the verbose mode of tcpdump lets the user additionally view the packet options of all IP packets. tcpdump monitors data traffic at a network adapter. The following examples use tcpdump in verbose mode to monitor the previous ping example.

```
# tcpdump -v
User level filter, protocol ALL, datacagram packet
tcpdump: listening on eth0
15:37:56.025267 isdn216-10.rz.uni-karlruhe.de > rzstud1.rz.uni-karlruhe.de:
icmp: echo request (tt 64, id 1284, optlen=40 RR{isdn216-10.rz-
```
