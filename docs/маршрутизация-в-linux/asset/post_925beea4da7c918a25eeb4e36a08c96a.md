
## -s Packetsize

The -s parameter can be used to send smaller or larger ICMP packets than the standard 64byte packet. This option combined with tcpdump (covered later) can be used to determined if IP datagrams are being fragmented, which is common in networks that contain various network topologies.

## -I Interface IP Address

The -I parameter forces the ICMP echo request out of the specified interface, which is very useful on multihomed hosts where there are multiple routes to the destination.

## Address Resolution Protocol (ARP)

The Address Resolution Protocol (ARP) maps Layer 3 IP addresses to Layer 2 MAC addresses. Understanding when and how ARP is used is important to fully utilize the arp command. Whenever a node wishes to send traffic to a particular IP address, it will use its own IP address and netmask to determine if the destination is on a directly connected network. If the destination address is not directly connected, the routing table is consulted. Assuming a route for the destination network exists (a default route can include the destination network), the host then determines the gateway for the routing entry. After the gateway is determined, an arp who-has request with the gateway's (router) address can be broadcast on the appropriate network interface, and the gateway will respond with its MAC address. The host will then direct traffic for the destination to the MAC address of the gateway.

Linux's tool to access the ARP table is the command arp. arp, like the ifconfig command, is provided in the net-tools distribution available at http://www.tazenda.demon.co.uk/phil/net-tools/.

arp, like ifconfig, is very useful without any parameters:

```
[root@lefty /root]# arp
Address              HWtype  HWaddress           Flags Mask    Iface
192.168.1.1          ether   00:20:78:CF:3D:66   C              eth0
speedy               ether   00:40:00:08:6A:72   C              eth0
```

The output includes the Layer 3 (IP) address, the type of network interface (HWtype), the MAC address (HWaddress), and the interface where the MAC address was learned. The Mask was used with early versions of Linux but is now no longer used. The Flags entry C reports that the entry is completed—that is, that the IP address is learned.

The arp output is not completely consistent: an incomplete entry is actually shown with an (incomplete) entry as opposed to any entry being made in the Flags column in the arp table:

```
[root@lefty /root]# arp
Address              HWtype  HWaddress           Flags Mask    Iface
192.168.1.5          (incomplete)                            eth0
192.168.1.1          ether   00:20:78:CF:3D:66   C              eth0
speedy               ether   00:40:00:08:6A:72   C              eth0
```

arp supports many parameters to assist in network troubleshooting.

## -a Host

The -a host parameter filters the arp command output to the specific host involved.

The host can be either the host name of the particular node or the node's IP address.

The following shows the MAC address assigned to 192.168.1.100:

```
[root@lefty /root]# arp -a 192.168.1.100
Address       HWtype  HWaddress     Flags Mask Iface
192.168.1.100 ether   00:20:58:CC:66:3D C       eth0
```

The -a host combined with the -d option discussed in the following section run on several Linux nodes on the same network and can help to quickly identify two hosts configured with the same IP address—the IP addresses will be the same, but the MAC address will be different.

## -H hwtype

The -H parameter specifies that only arp entries for the particular interface type should be printed. For example, to print all Ethernet entries, use

```
[root@lefty /root]# arp -H ether
Address       HWtype  HWaddress     Flags Mask Iface
192.168.1.1   ether   00:20:78:CF:30:66 C       eth0
speedy        ether   00:40:D0:08:6A:72 C       eth0
```

Or to see any Token Ring entries:

```
[root@lefty net]# arp -H tr
arp: in 2 entries no match found.
```

The media (hardware) types supported by the arp command are shown in Table 9.6.

### Table 9.6 Network Media Types Supported by Linux arp Command

| Media | Hardware Types Abbreviations |
|---|---|
| Adaptive Serial Line IP | Adaptive |
| Amateur NET/ROM | Netrom |
| Amateur ROSE | rose |
| Amateur X.25 | ax25 |
| ARCnet | arcnet |
| Ash | ash |
| Cisco HDLC | hdlc |
| Compressed Serial Line IP | cslip |
| Compressed Serial Line IP | cslip6 |
| 6 bit |  |
| Econet | ec |
| Ethernet | ether |
| Fiber Distributed Data Interface | fddi |
