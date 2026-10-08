
# ASSIGNMENT OF IP ADDRESSES 385

no access to a name server, you should additionally specify the option -n, so only the IP addresses are displayed and not the associated names.

## 13.4 Assignment of IP addresses

IP-addresses IP addresses consist (currently) of 32 bits and are usually written in '.dotted notation' (that is, one number per byte, separated by dots). The addresses are subdivided into a network part and a host part. Differently sized networks are available; an overview can be found in Table 13.1. In addition, there are addresses for special (experimental) services, and for multicasting (see also [rfc1112]).

The first bits of the IP address determine the membership in a network class. Depending on this class, the rest of the address is divided into a network number and a host number. Figure 13.4 shows this for the currently used address classes.

| Class | Address range | Number of computers | Default netmask |
|---|---|---|---|
| A | 1.0.0.0 – 127.0.0.0 | About 1.6 million | 255.0.0.0 |
| B | 128.0.0.0 – 191.255.0.0 | 65024 | 255.255.0.0 |
| C | 192.0.0.0 – 223.255.255.0 | 254 | 255.255.255.0 |
| D | 224.0.0.0 – 239.255.255.0 | Multicast addresses | |
| E | 240.0.0.0–255.255.255.255 | Reserved | |

Table 13.1 IP address ranges per network class.

| | 8 | 16 | 24 | 32 |
|---|---|---|---|---|
| 0 | Network ID | Host ID | Class A |
| 1 0 | Network ID | Host ID | Class B |
| 1 1 0 | Network ID | Host ID | Class C |
| 1 1 1 0 | Host group | Class D |

Figure 13.4 Structure of the subnet addresses.

Table 13.2 shows some examples. The network addresses are highlighted in bold. As a rule, only computers with the same network number should be connected to the same Ethernet cable. Equally, computers with the same network number should be located on the same side of a router.

| Class | IP address | Bit representation |
| --- | --- | --- |
| A | 10.0.0.32 | 00001010.00000000.00000000.00100000 |
| B | 128.14.58.60 | 10000000.00001110.01111010.00111100 |
| C | 192.9.150.202 | 11000000.00010101.10101010.11010100 |

**Table 13.2** Examples of IP addresses from different network classes.

These are the default splitting. You are requested to use only a small number of IP addresses with a special netmask (the number of bits used for the network addresses). This is called subnetting; see Section 13.5.1 for details.

You can not only specify the IP address as a group of four bytes, but also as an integer number, for example, telnet 2137064433 instead of 127.0.0.1. On the basis of an IP address a.b.c.d this number is calculated via the formula a*256²+b*256²+c*256+d. Input of an IP address by means of this formula can confuse even-boiled system administrators.

If your internal network is not to (continuously) connected to the Internet, it is often impossible to obtain an official IP address for all computers because the available address space is limited and may be nearly exhausted through the rapid growth of the Internet. This situation will change with the introduction of IPv6, which significantly increases the available space. For such cases, there are numbers reserved by the Internet (see Table 13.3) which are not routed in private networks. For this case too, [rfc1918] gives some hints on how to prevent all computers from being given a new IP address later. [rfc1627], points out the problems you can run into internal addresses.

| Network size | Reserved IP addresses |
| --- | --- |
| Class A | 10.0.0.0 – 10.255.255 |
| Class B | 172.16.0.0 – 172.31.255 |
| Class C | 192.168.0.0 – 192.168.255.255 |

**Table 13.3** Reserved address ranges.

This means to emphasize the character of the presented configurations, the necessary IP addresses can be entered into the corresponding script or into a configuration file. In the Red Hat distribution, IP addresses are stored in the file /etc/sysconfig/network; The S.U.E. distribution stores this information in the file /etc/rc.config.

The IP address can also be dynamically assigned during booting of a BOOTP request [rfc0952]. For this purpose, a BOOTP server or corresponding gateway may be configured in the local network which determines the IP address and passes it to the client. RFCs working on this subject are [rfc1497] and [rfc1542]. An extension of the BOOTP protocols is defined in [rfc2132] with DHCP (Dynamic Host Configuration Protocol). More about setup and operation of BOOTP server can be found in Chapter 2.

### 13.3.1 Netmask and broadcast address

The Internet Protocol differentiates between local computers in the same subnet and remote computers. A computer is in the same subnet if its address matches all bits of the broadcast address specified by the netmask.

In this case, membership in the same network can still be directly seen by the user. If you use subnetting (see also [rfc0940] and [rfc0501]) you must look at the bit masks. Subnetting is used to subdivide an assigned network internally and to separate the subnets by means of a router. Such a separation is recommended for reasons of reliability of networks that exceed a certain size. Another reason for subnetting could be that your provider has assigned you only 32 or 64 official IP addresses.

In subnetting, the boundary between network address and host address does not necessarily lie on a byte boundary. Thus, the network administrator is free to choose any arbitrary subdivision. This has the unfortunate effect that already scarce IP addresses are given away (one network address and one broadcast address for each subnet), so employing private addresses in the sense of [rfc1918] should be considered instead.

The counterpart to the above is supernetting (see [rfc1518] and [rfc1519]). Because of the exponential growth of the Internet, the routing tables of the routers have also grown very rapidly since a separate route had to be entered for every Class C network. Later on, individual providers were assigned whole bundles of consecutive networks for which only one entry per provider is needed. Each provider splits this range of numbers internally for the customers. Also, companies and other organizations are assigned two or more contiguous C networks if one network is not sufficient. This structure can then be almost arbitrarily subdivided by means of subnetting without any other network user having to take special measures.

## 13.4 All about ifconfig

The ifconfig program is used for management and activation of the appropriate kernel network interface. The first interface is eth0 for Ethernet cards and tr0 for Token Ring cards. The second interface is eth1 or tr1. The kernel itself only recognizes the first interface automatically; the second one is specified either by means of an adaptation in the file drivers/net/space.c or a kernel command line.

With ifconfig, interfaces can be stopped (down) or started (up). If ifconfig is called without parameters, it displays the status of the interfaces. If the name of an interface is specified as the parameter, only the status of the interface is shown. In addition, a series of further settings can be defined:

- arp specifies whether or not this interface uses ARP (Address Resolution Protocol). If ARP is not to be used, the option is prefixed with a minus sign (-). If you use Ethernet, you must use ARP, otherwise your computer cannot be reached in the network. This protocol is explained in more detail in Section 13.9.

- The Maximal Transfer Unit mtu is the maximum size of an IP packet transmitted via this device. For serial connections, a relatively small value should be specified because this reduces the answering times of interactive programs; for example, telnet transmits bytes per character. For file via ftp, however, a large MTU is better because it reduces the overhead; that is, the number of bytes used for headers and checksums instead of payload data. The mtu is determined by the employed medium. When using bridges between different network structures, the smallest MTU of all networks must be used. With the aid of fragmentation, routers can also transmit packets via media with a smaller packet size.

- On the basis of the specified IP address, ifconfig recognizes the network type and automatically determines the corresponding netmask. For purposes of subnetting, the parameter netmask can be used to specify your own netmask.
