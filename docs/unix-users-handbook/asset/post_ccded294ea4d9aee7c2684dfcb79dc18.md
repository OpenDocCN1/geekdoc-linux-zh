
(See the LAN Card Numbering subsection.)

| parameters | One or more of the following operating parameters: |
| :--- | :--- |
| up | Mark an interface "up". Enables interface after an ifconfig down. Occurs automatically when setting the address on an interface. Setting this flag has no effect if the hardware is "down". |
| down | Mark an interface "down". When an interface is marked "down", the system will not attempt to transmit messages through that interface. If possible, the interface will be reset to disable reception as well. This action does not automatically disable routes using the interface. |
| broadcast | (Inet only) Specify the address that represents broadcasts to the network. The default broadcast address is the address with a host part of all 1's. |
| debug | Enable driver-dependent debugging code. This usually turns on extra console error logging. |
| -debug | Disable driver-dependent debugging code. |
| ipdst | (NS only) This is used to specify an Internet host that is willing to receive IP packets encapsulating NS packets bound for a remote network. In this case, an apparent point-to-point link is constructed, and the address specified is taken as the NS address and network of the destination. |
| metric n | Set the routing metric of the interface to n. The default is 0. The routing metric is used by the routing protocol (see gated(1m)). Higher metrics have the effect of making a route less favorable; metrics are counted as additional hops to the destination network or host. |
| netmask mask | (Inet only) Specify how much of the address to reserve for subdividing networks into subnetworks or aggregating networks into supernets. Mask can be specified as a single hexadecimal number with a leading 0x, with a dot-notation Internet address, or with a pseudo-network name listed in the network table (see networks(4)). For subdividing networks into sub-networks, mask must include the network part of the local address, and the subnet part which is taken from the host field of the address. mask must contain 1's in the bit positions in the 32-bit address that are to be used for the network and subnet parts, and 0's in the host part. The 1's in the mask must be contiguous starting from the leftmost bit position in the 32-bit field. mask must contain at least the standard network portion, and the subnet field must be contiguous with the network portion. The subnet field must contain at least 2 bits. The subnet part after performing a bit-wise AND operation between the address and the mask must not contain all 0's or all 1's. For aggregating networks into supernets, mask must only include a portion of the network part. mask must contain contiguous 1's in the bit positions starting from the leftmost bit of the 32-bit field. |
| trailers | Request the use of a "trailer" link-level encapsulation when sending. If a network interface supports trailers, the system will, when possible, encapsulate outgoing messages in a manner that minimizes the number of memory-to-memory copy operations performed by the receiver. On networks that support the Address Resolution Protocol, this flag indicates that the system should request that other systems use trailers when sending to this host. Similarly, trailer encapsulations will be sent to other hosts that have made such requests. Currently used by Internet protocols only. See WARNINGS section. |
| -trailers | Disable the use of a "trailer" link-level encapsulation (default). |

## LAN Card Numbering

The name of an interface associated with a LAN card is lan, and its unitnumber is determined as follows. The LAN card installed first in the system is given interface unit number 0; the next LAN card installed is given interface unit number 1 and so on. When there are two or more LAN cards installed at the same time, interface unit numbers are assigned according to card positions in the backplane: the LAN card that appears "first" in the backplane is given the interface unit number $N_{r}$ the next LAN card in the backplane is given the number N+1.

The lanscan command can be used to display the name and unit number of each interface that is associated with a LAN card (see lanscan(1M)).

## Supernets

A supernet is a collection of smaller networks. Supernetting is a technique of using the netmask to aggregate a collection of smaller networks into a supernet. This technique is particularly useful for class C networks. A Class C network can only have 254 hosts. This can be too restrictive for some companies. For these companies, a netmask that only contains a portion of the network part can be applied to the hosts in these class C networks to form a supernet. This supernet netmask should be applied to those interfaces that connect to the supernet using the ifconfig command. For example, a host can configure its interface to connect to a class C supernet, 192.6, by configuring an IP address of 192.6.1.1 and a netmask of 255.255.0.0 to its interface.

## DIAGNOSTICS

Messages indicate if the specified interface does not exist, the requested address is unknown, or the user is not privileged and tried to alter an interface's configuration.

## WARNINGS

Currently, all HP 9000 systems can receive trailer packets but do not send them. Setting the trailers flag has no effect.

## SEE ALSO

netstat(1), lanconfig(1m), lanscan(1m) hosts(4), routing(7).

## netstat

![](img/75f39fc91296b889c0653851accdfd46_557_0.png)

**netstat - Display statistics related to networking.**

netstat(1)

**NAME**

netstat - show network status

**SYNOPSIS**

netstat [-aAn] [-f address-family] [system [core]]
netstat [-mMnrvs] [-f address-family] [-p protocol] [system [core]]
netstat [-gin] [-I interface] [interval] [system [core]]

**DESCRIPTION**

netstat displays statistics for network interfaces and protocols, as well as the contents of various network-related data structures. The output format varies according to the options selected. Some options are ignored when used in combination with other options.

Generally, the netstat command takes one of the three forms shown above:

- The first form of the command displays a list of active sockets for each protocol.
- The second form displays the contents of one of the other network data structures according to the option selected.
- The third form displays configuration information for each network interface. It also displays network traffic data on configured network interfaces, optionally updated at each interval, measured in seconds.

Options are interpreted as follows:

- **-a**
  Show the state of all sockets, including passive sockets used by server processes. When netstat is used without any options (except -A and -n), only active sockets are shown. This option does not show the state of X.25 programmatic access sockets. The option is ignored if the -g, -i, -I, -m, -M, -p, -r, -s or interval option is specified.
- **-A**
  Show the address of the protocol control block associated with sockets. This option is used for debugging. It does not show the X.25 programmatic access control blocks. This option is ignored if the -g, -i, -I, -m, -M, -p, -r, -s or interval option is specified.
- **-f address-family**
  Show statistics or address control block for only the specified address-family. The following address families are recognized: inet for AF_INET, and unix for AF_UNIX. This option applies to the -a, -A and -s options.
- **-g**
  Show multicast information for network interfaces. Only the address family AF_INET is recognized by this option. This option may be combined with the -i option to display both kinds of information. The option is ignored if the -m, -M or -p option is specified.
- **-i**
  Show the state of network interfaces. Interfaces that are statically configured into a system, but not located at boot time, are not shown. This option is ignored if the -m, -M or -p option is specified.
- **-I interface**
  Show information about the specified interface only. This option applies to the -g and -i options.
- **-m**
  Show statistics recorded by network memory management routines. If this option is specified, all other options are ignored.
- **-M**
  Show the multicast routing tables. When -s is used with the -M option, netstat displays multicast routing statistics instead. This option is ignored if the -m or -p option is specified.
- **-n**
  Show network addresses as numbers. Normally, netstat interprets addresses and attempts to display them symbolically. This option applies to the -a, -A, -i, -r and -v options.
- **-p protocol**
  Show statistics for the specified protocol. The following protocols are recognized: tcp, udp, ip, icmp, igmp, arp, and probe. This option is ignored if the -m option is specified.
- **-r**
  Show the routing tables. When -v is used with the -r option, netstat also displays the network masks in the route entries. When -s is used with the -r option, netstat displays routing statistics instead. This option is ignored if the -g, -m, -M, -i, -I, -p or interval option is specified.
- **-s**
  Show statistics for all protocols. When this option is used with the -r option, netstat displays routing statistics instead. When this option is used with the -M option, netstat displays multicast routing statistics instead. This option is ignored if the -g, -i, -I, -m, -p or interval option is specified.
- **-v**
  Show additional routing information. When -v is used with the -r option, netstat also displays the network masks in the route entries. This option only applies to the -r option.

The arguments system and core allow substitutes for the defaults, /stand/vmunix and /dev/kmem.

If no options or only the -A or -n option is specified, netstat
