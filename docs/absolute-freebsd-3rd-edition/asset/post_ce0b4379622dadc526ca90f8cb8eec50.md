
combination, enclose the address in square brackets, as in `[2001:db8:5c00:0:90ff:bad:c0de:cafe]:80`.

## IPv6 Subnets

IPv6 addresses have colons every 16 bits, so the obvious and natural ways to divide networks are at the /16, /32, /48, /64, /80, /96, and /112. The original IPv6 standards recommend subnetting only on these boundaries (repeating one of IPv4's greatest mistakes), but that's increasingly being rejected in favor of IPv4-style subnetting anywhere. IPv6 subnets are always expressed as a slash, also known as a prefix length, so you won't see a netmask like ffff.ffff.ffff.ffff:: analogous to IPv4.

ISPs are usually issued a /32 or /48 and are expected to issue end-user networks, such as a typical client, a /64 network. A /64 has $2^{64}$ subnets, or 18,446,744,073,709,551,616 addresses. If your home or office runs out of IP addresses, you need to stop networking individual blueberries.

When you subnet at 16-bit boundaries, each network has 65,536 subnets of the next smaller size. A /32 contains 65,536 /48 networks, and a /48 contains 65,536 /64 networks.

This is a long-winded way of explaining why I don't provide handy charts of IPv6 subnets and network size. Do an internet search for "IPv6 subnet calculator" to use one of the many on the internet.

## Link-Local Addresses

Addresses beginning with `fe8x::` (where $x$ is any hexadecimal character) are local to their interface. Every interface has such link-local addresses that are valid only on a specific local network. Even if an IPv6 network has no router, hosts on the local directly attached network can find each other and communicate using these local addresses. Link-local networks are always /64 subnets. You'll see identical IPv6 subnets on other interfaces and on networks completely disconnected from your network.

That’s okay. These addresses are local to the link. For example, here’s a link-local address from a test machine.

```
fe80::bad:c0de:cafe%vtnet0
```

The link-local address of this interface is `fe80::bad:c0de:cafe`. The trailing `%vtnet0` indicates that this address is local to the interface `vtnet0` and isn’t usable on any other interface on the machine. If your machine has an interface `vtnet1`, and a host on that network tries to reach the address `fe80::bad:c0de:cafe`, this machine will not respond. This particular address is valid only for hosts on the network segment directly attached to interface `vtnet0`.

You might note that the link-local address has a section in common with the public IPv6 address on this interface. That’s because an autoconfigured IPv6 address is usually calculated from the interface’s physical address; it doesn’t matter whether that autoconfigured address is public or local to the link.

### Assigning IPv6 Addresses

IPv6 clients on a /64 or larger network can normally autoconfigure their network through router discovery. Router discovery resembles a stripped-down DHCP service. The router broadcasts gateway and subnet information, and the hosts configure themselves to use it.

Modern versions of router discovery include very basic DHCP-style options, such as DNS servers. Not all IPv6 providers include these options in their router discovery configuration, however. If you want to provide sophisticated autoconfiguration for phones or diskless hosts, or if your provider doesn’t offer DNS information in their configuration, you’ll need to set up an IPv6 DHCP server.

Servers should not use IPv6 autoconfiguration. A server usually needs a static IP, even in IPv6.

Hosts on a network smaller than /64 must be manually configured.

The address `::1` always represents the local host and is assigned to the loopback address.

## TCP/IP Basics

Now that you have a simple overview of how the IP system works, let's consider the most common network protocols in more depth. The dominant transport protocol on the internet is the Transmission Control Protocol over Internet Protocol, or **TCP/IP**. Although TCP is a transport protocol and IP is a network protocol, the two are so tightly intertwined that they're generally referred to as a single entity.

We'll start with the simplest, **ICMP**, and proceed to **UDP** and **TCP**. All of these protocols run over both IPv4 and IPv6. While the versions of each protocol vary according to the underlying IP protocol, they behave essentially the same.

### *ICMP*

The Internet Control Message Protocol (ICMP) is the standard for transmitting routing and availability messages across the network. Tools such as `ping(8)` and `traceroute(8)` use ICMP to gather their results. IPv4 and IPv6 have slightly different versions of ICMP, sometimes called *ICMPv4* and *ICMPv6*.

While some people claim that you must block ICMP for security reasons, ICMP is just as diverse as the better-understood protocols TCP and UDP. Proper IPv4 network performance requires large chunks of ICMPv4. If you feel you must block ICMP, do so selectively. For example, blocking source quench messages breaks path maximum transmission unit (pMTU) discovery, which is like faceplanting into a crate of broken glass and rusty nails. If you don't understand that last sentence, don't block ICMP.

IPv6 dies without ICMPv6, as IPv6 doesn't support packet fragmentation. If you use IPv6, never block ICMPv6 as a whole. Blocking parts of ICMPv6 without destroying your network requires careful research and testing.

### *UDP*

The User Datagram Protocol (UDP) is the most bare-bones data transfer protocol that runs over IP. It has no error handling, minimal integrity verification, and no defense whatsoever against data loss. Despite these drawbacks, UDP can be a good choice for particular sorts of data transfer, and many vital internet services rely on it.

When a host transmits data via UDP, the sender has no way of knowing whether the data ever reached its destination. Programs that receive UDP data simply listen to the network and accept what happens to arrive. When a program receives data via UDP, it cannot verify the source of that data—while a UDP packet includes a source address, this address is easily faked. This is why UDP is called *connectionless*, or *stateless*.

With all of these drawbacks, why use UDP at all? Applications that use UDP most often have their own error-correction handling methods that don’t mesh well with the defaults provided by protocols such as TCP. For example, simple client DNS queries must time out within just a few seconds or the user will call the helpdesk and whine. TCP connections time out only after two minutes. Since the computer wants to handle its failed DNS requests much more quickly, simple DNS queries use UDP. In cases where DNS must transfer larger amounts of data (for example, for zone transfers), it intelligently switches to TCP. Real-time streaming data, such as video conferencing, also uses UDP. If you miss a few pixels of the picture in a real-time video conference, retransmitting that data would simply add congestion. You can’t go back in time to fill in those missing chunks of the picture, after all! You’ll find similar reasoning behind almost all other network applications that use UDP.

Because the UDP protocol itself doesn’t return anything when you connect to a port, there’s no reliable way to remotely test whether a UDP port is reachable (although tools like `nmap` try to do so).

UDP is also a *datagram* protocol, meaning that each network transmission is complete, self-contained, and received as a single integral unit. While the application might not consider a single UDP packet a complete request, the network does. TCP is entirely different.

### *TCP*

The Transmission Control Protocol (TCP) includes such nifty features as *error correction* and *recovery*. The receiver must acknowledge every packet it gets; otherwise, the sender will retransmit any unacknowledged packets. Applications that use TCP can expect reliable data transmission. This makes TCP a *connected*, or *stateful*, protocol, unlike UDP.

TCP is also a *streaming* protocol, meaning that a single request can be split amongst several network packets. While the sender might transmit several chunks of data one after the other, the recipient could receive them out of order or fragmented. The recipient must keep track of these chunks and assemble them properly to complete the network transaction.

For two hosts to exchange TCP data, they must set up a channel for that data to flow across. One host requests a connection, the other host responds to the request, and then the first host starts transmitting. This setup process is known as the *three-way handshake*. The specifics are not important right now, but you should know that this process happens. Similarly, once transmission is complete, the systems must do a certain amount of work to tear down the connections.

TCP is commonly used by applications—such as email programs, FTP clients, and web browsers—for its fairly generic set of timeouts and transmission features.

### How Protocols Fit Together

You can compare the network stack to sitting with your family at a holiday dinner. The datalink layer (ARP, in the case of IPv4 over Ethernet) lets you see everyone else at the table. IP gives every person at the table a unique chair, except for the three young nephews using piano bench NAT. ICMP provides basic routing information, such as, “The quickest way to the peas is to ask Uncle Chris to hand them to you.” TCP is where you hand someone a dish and the other person must say, “Thanks,” before you let go. Finally, UDP is like tossing a roll at Aunt
