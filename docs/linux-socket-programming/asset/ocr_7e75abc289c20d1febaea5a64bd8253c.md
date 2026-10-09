The `inet_pton()` call converts the alphanumeric address in `prsnt` into the network byte-ordered binary form and places the result in `buf`. The `inet_ntop()` call does the reverse. Parameters `domain` and `len` define the network (`AF_INET` or `AF_INET6`) and `prsnt` array length, respectively.

# ## Converting Raw Sockets to IPv6

If you are using a UDP or TCP socket, that's all you have to do. However, if you are programming a raw or ICMP socket, you have to use special new record formats. Raw-6 and ICMP6 include new or revised fields to support the extra capabilities.

The IPv6 header is much simpler than the IPv4 header and only doubles the overhead (40 bytes versus 20 bytes). The header is also a fixed size because no options are allowed (please note that this is not quite true, as the next section describes). The IP (for raw sockets) can be defined as follows in network byte order:

```
```c
 /***************************************************************/
 /** IPv6 Packet definition ***/
 /***************************************************************/
 union IPv6_Address
 {
 unsigned char u8[16];
 unsigned short int u16[8];
 unsigned long int u32[4];
 unsigned long long int u64[2];
 };
 struct IPv6_Header
 {
 unsigned int version:4; /* The IP version (6) */
 unsigned int priority:4;
 unsigned int flow_label:24;
 unsigned int payload_len:16; /* bytes following header */
 unsigned int next_header:8; /* protocol (6 for TCP) */
 unsigned int hop_limit:8; /* same as TTL */
 union IPv6_Address source;
 union IPv6_Address dest;
 };
```
```

Only three of the fields require more explanation. The `priority` field is an experimental field that sets the priority of the packet. If the network becomes congested, routers may hold or drop lower-priority packets. By default, all packets are `priority` zero.

The `flow_label` field is also experimental and works with `priority`. The flow is a sequence of packets that move from source to destination through a series of routers. `flow_label` helps the routers determine any special handling. A message has only one `flow_label`; after it is selected, the flow value does not change for all packets in the flow. You can set the `priority` and `flow_label` when you bind the socket address using the optional `sin6_flowinfo` field in `sockaddr_in6`.

The last field, `payload_len`, can be zero to indicate a huge packet. A one gigabit (or even 100Mbit) network sending small packets (less than 100KB) is a waste of bandwidth. Set this field to