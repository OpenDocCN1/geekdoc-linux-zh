
# THE netstat PROGRAM 393

| Flag | Description |
| --- | --- |
| A | The interface receives all multicast addresses |
| B | Broadcasts are allowed |
| D | Debugging is on |
| L | This is a loopback interface |
| M | All packets are received (promiscuous mode) |
| N | No trails are generated |
| O | This interface does not use ARP |
| P | The interface is a point-to-point connection |
| R | The interface is running |
| U | The interface is up |

Table 13.4 Flags in netstat -i.

- -c regenerates the requested list each second, so that changes can be detected. The program must be terminated with Ctrl-C.
- -n prevents the output of host name and service, so only the numerical values are displayed. Thus, the ‘reverse lookup’ in the name server is omitted, which may lead to long timeouts and increases network load.
- -o displays the timer status.

- - Under UNIX, -r is equivalent to route, the kernel routing tables are displayed. Under other UNIX systems, where route cannot be used to display the routing tables of the kernel, you must always use netstat -r.
- -t displays information on TCP sockets.
- -u displays information on UDP sockets.
- -w displays information on RAW sockets.
- -x displays information on UNIX sockets.

As long as your computer is not networked, you can shut down your computer without problems. If a serial terminal is connected to your computer, you should verify before each shutdown, for example by means of w and ps aux, whether a user is active on that terminal. If however, your computer is employed as a network server, you must also consider other network connections. All active connections can be displayed via netstat -a.

# 13.5 The Address Resolution Protocol (ARP)

On the Ethernet level, there are two types of connections between computers: packets can be sent directly to a computer, that is, to the hardware address (MAC or Media Access Control) of its Ethernet card, or to all computers in the local network (broadcast). If a computer is to be addressed, the Ethernet address must be available. For transport within the local network, each IP packet is equipped with an additional header into which the hardware addresses of sender and receiver are entered.

Initially, however, only the IP address of the receiver is available. The sender sends a broadcast to all local computers and looks for the Ethernet address that belongs to the required IP address. The underlying Address Resolution Protocol is defined in [rfc0826]. The answer (correlation between IP address and hardware address) of the required receiver is stored in the ARP cache, which makes interrogation need not be continuously repeated. To ensure that, after replacing a computer, the entries in the ARP cache expire after a short time and are recreated.

The arp program can be used to display and modify this ARP cache. This can be useful if two computers (with different hardware addresses) they can use the same IP address. With other means, errors are difficult to diagnose. ARP cache entries are displayed by means of the option -a (see List 13.7). Entries can be deleted with -d and added with -s.

```
(Linux):# arp -a
Address         HW type HW address Flags Mask
192.168.3.161 10Mbps Ethernet 00:00:83:21:D1:FA C *
192.168.3.150 10Mbps Ethernet 10:00:5A:B3:01:E9 C *
```

List 13.7 The arp program.

A further application of the arp program is the routing of IP packets, for example to a computer that is connected via SLIP or PPP (proxy ARP). The local computer accepts packets for the remote computer and forwards them via the SLIP or PPP connection. Thus, there is no more need to split off a subnet, which would be a waste of precious IP addresses.

On a computer which functions as a router between Ethernet and SLIP or PPP, the ARP cache is modified in such a way that it propagates its own Ethernet address as being valid for the dial-up computer. It is obtained by

- Some Some drivers support the promiscuous mode in which all packets are read by the Ethernet. This is important for network monitoring, but it is also a security problem since all traffic, including passwords, can be recorded.

If you are running PPP, which has almost completely replaced SLIP by now, you can specify the proxyarp option and pppd does all that is needed.

# TCP/IP basics

# 14

Chapter 13 has shown how to configure a LINUX computer for participation in a TCP/IP-based network. This chapter will introduce the individual protocols and their use within within the network. This should enable you to understand the functioning of a TCP/IP network. As already shown in Figure 13.2, the hardware connections form the basis for a series of protocol layers, whose interaction will now be explained in more detail.

# 14.1 Protocols

The Internet is based on a series of protocols which guarantee orderly data exchange between computers. The numbers of these protocols are defined in the file /etc/protocols (Listing 14.1). It is extremely improbable that you will ever be called on to modify this file.

Essentially, four protocols are used whose existence in the kernel is also signalled by LINUX during booting:

```
ip      0      IP      # internet protocol, pseudo number
icmp    1      ICMP   # internet control message protocol
igmp    2      IGMP   # internet group multicast protocol
gggp     3      GGP     # gateway-gateway protocol
tcp     6      TCP     # transmission control protocol
pup     12     PUP     # PARC universal packet protocol
udp     17     UDP    # user datagram protocol
idp    22     IDP    # WhatisThis?
raw     255    RAW     # RAW IP interface
```

Listing 14.1 Internet protocols (/etc/protocols).

- IP, the Internet Protocol, serves as a basis for TCP and UDP. It is a connectionless protocol which does not contain any mechanisms for guaranteeing data transfer. The only thing required from the implementation is a 'best effort' when forwarding the packets. Furthermore, the quality of a connection can be improved by means of ICMP. The protocol is defined in [rfc0791].

- ICMP, the Internet Control Message Protocol, is used for the exchange of messages between computers on a very low level. This protocol is often implemented in the kernel itself. The individual message types of icmp are defined in [rfc0792].

- TCP (Transmission Control Protocol), [rfc0793], is a connection-oriented protocol which is slower.

- UDP (User Datagram Protocol). [rfc0768], a connectionless protocol which is faster.

# PROTOCOLS 399

Depending on the protocol, the application data are equipped with the header. These are defined in /etc/services (Listing 14.2).

| tcmux | 1/tcp | # TCP port service multiplexer |
| echo | 7/tcp | |
| echo | 7/udp | |
| discard | 9/tcp | sink null |
| discard | 9/udp | sink null |

Listing 14.2 Excerpt from the file /etc/services.
