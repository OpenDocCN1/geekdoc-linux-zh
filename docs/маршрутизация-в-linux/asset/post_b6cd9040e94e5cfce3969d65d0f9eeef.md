
## Table 9.1 Network Topology and Maximum Transmission Unit

| Topology | MTU |
|---|---|
| Ethernet | 1500 |
| Fiber Distributed Data Interface (FDDI) | 4352 |
| Point-to-Point (PPP) | 1500 |
| Serial Line IP (slip) | 1006 |
| Token Ring | 4464 |

Lines 4 through 6 report traffic statistics that are extremely useful in troubleshooting networking problems. Here, there seems to be a high number of collisions based on the amount of traffic, which could imply a mismatch between a half-duplex and full-duplex port with the Linux router and the Ethernet switch. The final line reports the resources used by the network interface card for low-level device driver support. This particular NIC uses interrupt 10 to speak to the CPU and has a memory segment starting at 0xb800.

Due to Ethernet’s popularity, the ifconfig output just described is very typical of what is found in most enterprise networks, but a closer examination of other hardware supported by Linux shows Linux’s wide support of network topologies.

## Hardware Types

Table 9.2 lists hardware types supported by the Linux operating system.

## Table 9.2 Network Media (Hardware) Types Supported by Linux and ifconfig

| Media | hwtype abbreviation |
|---|---|
| Adaptive Serial Line IP | Adaptive |
| Amateur NET/ROM | netrom |
| Amateur ROSE | rose |
| Amateur X.25 | ax25 |
| ARCnet | arcnet |
| Ash | ash |
| Cisco HDLC | hdlc |
| Compressed Serial Line IP | cslip |
| Compressed Serial Line IP 6 bit | cslip6 |
| Econet | Ec |
| Ethernet | ether |
| Fiber Distributed Data Interface | fddi |
| Frame Relay Access Device | frad |
| Frame Relay DLCI | dlci |
| High-Performance Parallel Interface | hippi |
| IP in IP Tunneling | tunnel |
| IPv6 in IPv4 Tunneling | sit |
| IrLAP | irda |
| LAPB | lapb |
| Local Loopback | loop |
| Point-to-Point Protocol | ppp |
| Serial Line IP | slip |
| Serial Line IP 6 bit | slip6 |
| Token Ring | tr |

A closer look at the more common interfaces follows.

### Serial Line IP—slip

slip (see RFC 1055, "A Nonstandard For Transmission Of IP Datagrams Over Serial Lines: Slip") is a serial connection-oriented protocol that has been replaced with PPP in most networks. Variants of slip that are supported under Linux include cslip, which is a compressed serial line IP based on the compression techniques described in RFC 1144, "TCP/IP Headers for Low-Speed Serial Links," also known by the author's name: Van Jacobson Compression. Another variant is slip6 and a compressed version of slip6, aptly named cslip6.

### Point-to-Point Protocol (PPP)

PPP is the de facto standard for serial link connections and has moved into other networking topologies, including IP over SONET. PPP (covered thoroughly in Chapter 7, "Kernel Support Tools").

### IP over IP Tunneling (IPIP)

IP over IP tunneling is often used for connecting autonomous networks through a transit network. IP over IP also can be used for creating virtual private networks (VPNs).

### Logical Loopback Device—Loop

Loopback interfaces exist to allow applications that require network connections to communicate with services residing on the local host without requiring or passing through a physical interface.

### Token Ring (TR)—(IEEE 802.5)

Token Ring, which operates at 4- or 16Mbps, had an early advantage over Ethernet of not relying on a broadcast domain. This advantage has been overcome by Ethernet's speed increases and Ethernet switching technology. However, Token Ring is still supported in many organizations—especially industries such as banking and financial institutions that IBM has strongly penetrated. (IBM sold a lot of Token Ring given that their early mainframes did not support Ethernet.)

Returning to ifconfig's output listed previously, notice the IP address is IP version 4. In addition to IPv4, Linux also supports other protocols and their addressing. Some of the more popular protocols and ifconfig's corresponding output are shown in Table 9.3.

## Table 9.3 Linux and ifconfig Protocols Supported

| Protocol | ifconfig abbreviation | Reference |
|---|---|---|
| IPv6 | inet6 | RFC 2373, "IP Version 6 Addressing Architecture" |
| Amateur [radio] X.25 | ax25 | AX.25 Amateur Packet-Radio Link Layer Protocol Version 2.2, November 1997 http://www.tapr.org/tapr/html/Fax25.html |
| Internetwork Packet Exchange | ipx | Novell http://www.novell.com/ |
| AppleTalk Datagram Delivery Protocol | ddp | "Inside Macintosh" by Apple Computers http://developer.apple.com/techpubs/mac/Networking/OT-Networking/WOT-66.html |

## Configuration Using ifconfig

ifconfig is also used to configure Linux network interfaces. Most Linux distributions have text or X Windows-based wrappers to initially fill configuration tables used by Linux during bootup, which are then used with the ifconfig command to configure the network interface for use. The commands covered here will have immediate effects on network configuration; however, it is still necessary to make the appropriate changes to configuration and network startup scripts, which is not covered here. Because configuration changes using the ifconfig command are immediate, the command can interrupt or even stop network traffic to and from the Linux node.

### Bringing Interfaces Up and Down

Likely the most basic and useful configuration command using ifconfig is shutting down and bringing up an interface. This could be performed to ensure no network connections are made during a software upgrade. It is also often the first set taken when the NIC is suspected of having trouble. To shut eth0 down, use

```
[root@fty /root]#ifconfig eth0 down
```
