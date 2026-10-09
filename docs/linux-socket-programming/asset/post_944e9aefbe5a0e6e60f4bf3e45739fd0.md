
## ICMP Codes

Table A.9 shows the different types of ICMP [RFC792] packets and what they mean.

| Type | Code | Description |
|---|---|---|
| 0 | 0 | Echo reply |
| 3 | | Destination unreachable |
| | 0 | Network unreachable |
| | 1 | Host unreachable |
| | 2 | Protocol unreachable |
| | 3 | Port unreachable |
| 4 | | Fragmentation needed but DF bit set |
| 5 | | Source route failed |
| 6 | | Destination network unknown |
| 7 | | Destination host unknown |
| 8 | | Source host isolated (obsolete) |
| 9 | | Destination network administratively prohibited |
| 10 | | Destination host administratively prohibited |
| 11 | | Network unreachable for TOS |
| 12 | | Host unreachable for TOS |
| 13 | | Communication administratively prohibited |
| 14 | | Host precedence violation |
| 15 | | Precedence cutoff in effect |
| 4 | 0 | Source quench—gateway requesting the host to reduce transfer rate |
| 5 | | Redirect |
| | 0 | Redirect for network |
| | 1 | Redirect for host |
| | 2 | Redirect for type-of-service and network |
| | 3 | Redirect for type-of-service and host |
| 8 | 0 | Echo request |
| 9 | 0 | Router advertisement |
| 10 | 0 | Router solicitation |
| 11 | | Time exceeded |
| | 0 | TTL equals 0 during transit |
| | 1 | TTL equals 0 during fragment reassembly |
| 12 | | Parameter problem |
| | 0 | IP header bad |
| | 1 | Required option missing |
| 13 | 0 | Timestamp request |
| 14 | 0 | Timestamp reply |
| 15 | 0 | Information request |
| 16 | 0 | Information reply |
| 17 | 0 | Address mask request |
| 18 | 0 | Address mask reply |

### IPv4 Multicast Allocation

Table A.10 defines the current multicast address allocation [RFC2365] in spectrum order.

**Table A.10, Proposed Multicast Allocation**

| Address Range | Scope | Typical TTL |
|---|---|---|
| 224.0.0.0–224.0.0.255 | Cluster | 0 |
| 224.0.1.0–238.255.255.255 | Global | <= 255 |
| 239.0.0.0–239.191.255.255 | (undefined) | |
| 239.192.0.0–239.195.255.255 | Organization | < 128 |
| 239.196.0.0–239.254.255.255 | (undefined) | |
| 239.255.0.0–239.255.255.255 | Site | < 32 |

### Proposed IPv6 Address Allocation

Table A.11 lists the proposed IPv6 address allocation in bits.

**Table A.11, Proposed IPv6 Address Allocation**

| Allocation | Address Prefix |
|---|---|
| (reserved) | 0000 0000 |
| (unassigned) | 0000 0001 |
| NSAP | 0000 001 |
| IPX | 0000 010 |
| (unassigned) | 0000 011 |
| (unassigned) | 0000 1 |
| (unassigned) | 0001 |
| Aggregate global unicast addresses | 001 |
| (unassigned) | 010 |
| (unassigned) | 011 |
| (unassigned) | 100 |
| (unassigned) | 101 |
| (unassigned) | 110 |
| (unassigned) | 1110 |
| (unassigned) | 1111 0 |
| (unassigned) | 1111 10 |
| (unassigned) | 1111 110 |
| (unassigned) | 1111 1110 0 |
| Link-local unicast address | 1111 1110 10 |
| Site-local unicast address | 1111 1110 11 |
| Multicast address | 1111 1111 |

## ICMPv6 Codes

Table A.12 shows the new ICMPv6 [RFC2463] for IPv6.

**Table A.12, ICMPv6 Code Descriptions**

| Type | Code | Description |
|---|---|---|
| 1 | | Destination unreachable |
| | 0 | No route to destination |
| | 1 | Administratively prohibited (firewall filter) |
| | 2 | Not a neighbor (incorrect strict source route) |
| | 3 | Address unreachable (general) |
| | 4 | Port unreachable |
| 2 | 0 | Packet too big |
| 3 | | Time exceeded |
| | 0 | Hop limit exceeded during transit |
| | 1 | Fragment reassembly time exceeded |
| 4 | | Parameter problem |
| | 0 | Erroneous header field |
| | 1 | Unrecognized next header |
| | 2 | Unrecognized option |
| 128 | 0 | Echo request (ping) |
| 129 | 0 | Echo reply (ping) |
| 130 | 0 | Group membership query |
| 131 | 0 | Group membership report |
| 132 | 0 | Group membership reduction |
| 133 | 0 | Router solicitation |
| 134 | 0 | Router advertisement |
| 135 | 0 | Neighbor solicitation |
| 136 | 0 | Neighbor advertisement |
| 137 | 0 | Redirect |

### IPv6 Multicast Scope Field

Table A.13 defines the different values for the scope field in the multicast IPv6 addresses.

**Table A.13, IPv6 Multicast Scope Field Descriptions**

| Scope | Range | Description |
|---|---|---|
| 0 | (undefined) | |
| 1 | Node | Local on the same host (like `127.0.0.1`). |
| 2 | Link | Messages stay within the router's group. The routers never let these messages pass through. |
| 3–4 | (undefined) | |
| 5 | Site | As defined by the network administrators, the messages stay within the site's locality. |
| 6–7 | (undefined) | |
| 8 | Organization | As defined by the network administrators, the messages stay within the organization's locality. |
| 9–13 | (reserved) | |
| 14 | Global | All routers permit messages to pass through the global network until they expire. |
| 15 | (reserved) | |

### IPv6 Multicast Flags Field

Table A.14 shows the currently defined flag fields for IPv6 multicast addresses.

**Table A.14, IPv6 Multicast Flags Field Descriptions**

| Bit # | Description |
|---|---|
| 0 | Transience |
| | 0= well known address |
| | 1= transient address |
| 1 | (reserved) |
| 2 | (reserved) |
| 3 | (reserved) |

## Appendix B. Networking API

### In This Appendix

- Connecting to the Network
- Communicating on a Channel
- Terminating Connections
- Network Data Conversions
- Network Addressing Tools
- Socket Controls

This appendix groups all the networking library and system calls.

### Connecting to the Network

The Sockets API provides tools to help you create sockets and connect to other hosts. This section describes the API relevant to socket creation and connection.

#### socket()

*socket()* creates a bidirectional channel that typically connects with the network. You can use this channel with network-specific system calls or general file I/O.

#### Prototype

```c
#include <resolv.h>
#include <sys/socket.h>
#include <sys/types.h>
int socket(int domain, int type, int protocol);
```

#### Return Value

If successful, the call returns a valid socket descriptor. Otherwise, the result is less than zero. Check *errno* for more information about the error.

#### Parameters

| Parameter | Description |
|---|---|
| *domain* | Selects the network protocol for socket (see Appendix A, "Data Tables"). |
| *type* | Selects the network layer (see Appendix A). |
| *protocol* | Usually zero (see Appendix A). |

#### Possible Errors

| Error | Description |
|---|---|
| EPROTONOSUPPORT | The protocol *type* or the specified *protocol* is not supported within this domain. |
| ENFILE | Not enough kernel memory to allocate a new socket structure. |
| EMFILE | Process file table overflow. |
| EACCES and ENOBUFS | Permission to create a socket of the specified *type* or *protocol* is denied. |
| ENOMEM | Insufficient memory is available. The socket cannot be created until sufficient resources are freed. |
| EINVAL | Unknown *protocol* or protocol family not available. |

#### Examples

```c
/*** Create a TCP socket ***/
int sd;
sd = socket(PF_INET, SOCK_STREAM, 0);

/*** Create an ICMP socket **/
int sd;
sd = socket(PF_INET, SOCK_RAW, htons(IPPROTO_ICMP));
```
