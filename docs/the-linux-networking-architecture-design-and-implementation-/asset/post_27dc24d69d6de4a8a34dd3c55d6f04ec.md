
## 14.2 Implementing the Internet Protocol

```
secure_redirects accepts ICMP redirect messages.
accept_source_route accepts Source Route packets.
p_filter disables the sender IP address check.
proxy_arp supports an ARP proxy.
log_martians enables or disables the logging of “strange” addresses (“Martians”)—see Section 16.2.2.
forwarding enables this network device to forward packets.
mc_forwarding enables multicast routing or forwarding over this IP network device.
```

## 14.2.5 Auxiliary Functions for the Internet Protocol

The functions introduced in the previous sections operate mainly in the data path of the Internet Protocol: They process incoming IP packets. In addition to these there are other things to be done in the Internet Protocol that do not directly relate to socket buffers or IP packets. These auxiliary functions are introduced below.

Managing Transport Protocols The Internet Protocol operates on the network layer and offers an unreliable datagram service for the transport layer. In general, the TCP and UDP protocols are used in the transport layer. However, a layer-based architectural model should also allow us to use our own protocols. The Linux architecture allows us to do that. You can register and use new protocols on top of the IP layer. With kernel modules, this represents a flexible and highly dynamic property of the Linux network architecture.

The Linux kernel includes two functions, inet_add_protocol() and inet_del_protocol(), which will be described below, to manage transport-layer protocols. Appendix F includes an example for a rudimentary transport protocol, which does nothing but output the length of incoming transport-layer PDUs.

```
inet_add_protocol() net/ipv4/protocol.c
```

All protocols arranged immediately on top of the Internet Protocol are managed in a hash table, inet_protos, inet_add_protocol(prot) registers a new protocol for the transport layer and adds it to the inet_protos hash table. The required protocol information is passed in the struct structure of the type inet_protocol (as shown in Figure 14-5)

handler() is a function pointer to the entry function of the transport protocol (handling routine), for example tcp_v4_rcv() for TCP. The parameters passed here include the socket buffer and the length of the transport-layer PDU. Appendix F includes an example of a very simple transport protocol. All it does is output the length of a PDU.

err_handler() is a handling routine for error cases. It is invoked only once in the current implementation, in the method icmp_unreach().

![](img/5a25b942ec3329b8799f2b5f0de564f6_272_0.png)

next is used to link inet_protocol structures in a hash table.
id the protocol identifier of the registered protocol. In the future, if an IP packet with this identifier in the protocol field of the IP packet header arrives, it is passed to the handler() handling routine. If several protocols with the same id are registered, a copy of the socket buffer is passed to each of these protocols.
The copy specifies whether another protocol is registered with the same protocol ID. If a protocol with the same protocol ID is already registered when you register a new protocol, then the new protocol is also added to the hash table; and the copy bit of all previous protocols with the same ID is set to one. In this case, all protocols with the same ID get a copy of the packet.

data points to private data of the protocol, if present. However, it is not used by any of the implemented protocols (TCP, UDP, ICMP, and IGMP).
names stores of the protocol in a string.

The Linux kernel currently implements four protocols on the transport layer, where only TCP and UDP are actually true transport protocols. Though ICMP and IGMP also use IP to exchange data, they are normally thought of as belonging to the network layer.

```
inet_del_protocol()
```

```
net/ipv4/protocol.c
```

inet_del_protocol(prot) removes the protocol, together with the passed pointer to an inet_protocol structure, from the hash table inet_protos. If there is a second protocol with the same protocol ID, then the copy bit of this protocol is checked and deleted, if applicable.

## Useful Functions

```
inet_ntoa()
```

```
net/ipv4/utils.c
```

inet_ntoa(in) converts the IP address into the dotted decimal form, which is easier to read for humans (i.e., the 32-bit address 0x810D2A75 is converted into the string 129.13.42.117.

```
inet_aton()
```

```
net/ipv4/utils.c
```

inet_aton(str) converts the string str into a 32-bit ip address.

## 14.3 IP OPTIONS

When a packet is sent to the IP layer, then it normally includes all required information in the packet protocol header. However, there could be times when packets require additional information in the protocol header—for example, for diagnostics purposes, or if a packet's path across the Internet is specified before it is sent. For these purposes, an Option field with variable length can be added to each IP packet header. All guidelines for these IP options are described in [Post81c].

## 14.3.1 Standardized IP Packet Options

Figure 14–9 shows that the IP packet options are appended to the end of an IP header. The length of the Option field is variable, and the end of a packet header has to be aligned to a 32-bit boundary, so an additional padding field of the appropriate length is added (and set to 0 by default). "variable" also means that the packet options can be left out, if they are not required. The Option field can take one or several packet options, where an option can be given in either of two formats:

- One single byte describes only the option type. The length of these options is exactly one byte.

The first byte includes the option type, and the second byte contains the length of this packet option. The following bytes include the actual data of that option.

The byte stating the length of the packet option in the second case includes the number of data bytes. The first two bytes are not counted. The option type in the first byte is composed as follows:

The (1-bit) copy flag is required for packet fragmentation. If a packet has to be fragmented, then this bit sets whether this option has to appear in all fragments or may be set in the first fragment onlyThe option class is represented by 2 bits. The (5-bit) option number shows the length of a packet option implicitly (i.e., we can see whether the next byte belongs to the next option). Table 14–1 lists all packet options defined in RFC 791, including their lengths and option classes. There are four option classes in total, but only two are currently used. Option 0 includes packet options for control and management; option 2 includes debugging and measurement options. Option class 1 and 3 are reserved for future packet-option classes.

> FIGURE 14–9 The packet header.

TABLE 14–1 Defined IP options.

| Class | Number | Length | Name |
|---|---|---|---|
| 0 | 0 | | End of Option List |
| 0 | 1 | | No Operation |
| 0 | 2 | | Security |
| 0 | 3 | var | Loose Source Routing |
| 0 | 9 | var | Strict Source Routing |
| 0 | 7 | var | Record Route |
| 0 | 8 | 4 | Stream ID |
| 2 | 4 | var | Timestep |

We will discuss each of these packet options in the following sections.

### End of Option List

Bit sequence:

```
70000000
```

This packet option marks the end of a series of options: it is appended to the last packet option and must never be between any other pair of options. The End-of-Option-List option is superfluous if the end of the option list is aligned at a 32-bit boundary. (See Figure 14–9). The question mark at the beginning of this bit sequence corresponds to the copy flag, which was described above. If fragmentation is necessary, then this option can be copied, inserted or deleted, depending on the number of packet options in the fragments of an IP datagram. It has to be inserted into a fragment—for example, if only a part of the original options has to be copied, and the end of the new option no longer matches the 32-bit boundary.

### No Operation

Bit sequence:

```
20000001
```

No Operation can be between any two packet options, for example to let the second option begin at a 32-bit boundary. If fragmentation is necessary, then this option can be copied, inserted or deleted. Like the End-of-Option List option, this option can always be inserted into a fragment, if only some of the original options are copied and if a packet option must begin at a 32-bit boundary.

### Security

Bit sequence:
