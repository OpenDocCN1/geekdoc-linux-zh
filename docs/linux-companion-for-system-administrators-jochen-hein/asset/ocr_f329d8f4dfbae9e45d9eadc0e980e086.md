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

+   3 Some drivers support the promiscuous mode in which all packets are read by the Ethernet. This is important for network monitoring, but it is also a security problem since all traffic, including passwords, can be recorded.