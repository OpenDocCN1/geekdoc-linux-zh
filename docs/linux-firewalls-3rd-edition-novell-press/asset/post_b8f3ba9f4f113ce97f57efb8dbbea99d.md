
if [ "$CONNECTION_TRACKING" = '1' ]; then
$IPT -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
$IPT -A OUTPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
# Using the state module alone, INVALID will break protocols that use
# bi-directional connections or multiple connections or exchanges,
# unless an ALG is provided for the protocol. At this time, FTP and
# IRC are the only protocols with ALG support.

$IPT -A INPUT -m state --state INVALID -j LOG \
     --log-prefix 'INVALID input: '
$IPT -A INPUT -m state --state INVALID -j DROP

$IPT -A OUTPUT -m state --state INVALID -j LOG \
     --log-prefix 'INVALID output: '
$IPT -A OUTPUT -m state --state INVALID -j DROP
fi

### Source Address Spoofing and Other Bad Addresses

This section establishes some INPUT chain filters based on source and destination addresses. These addresses will never be seen in a legitimate incoming packet from the Internet.

At the packet-filtering level, one of the few cases of source address spoofing that you can identify with certainty as a forgery is your own IP address. This rule drops incoming packets claiming to be from you:

```
# Refuse spoofed packets pretending to be from
# the external interface's IP address
$IPT -A INPUT -i $INTERNET -s $IADD -j DROP
```

There is no need to block outgoing packets destined to yourself. They won't return, claiming to be from you and appearing to be spoofed. Remember, if you send packets to your own external interface, those packets arrive on the loopback interface's input queue, not on the external interface's input queue. Packets containing your address as the source address never arrive on the external interface, even if you send packets to the external interface.

> **FIREWALL LOGGING**
> The -j LOG target enables logging for packets matching the rule. When a packet matches the rule, the event is logged in /var/log/messages, or wherever you've defined messages of the specified priority to be logged.

As explained in Chapter 1 and Chapter 2, private IP addresses are set aside in each of the Class A, B, and C address ranges for use in private LANs. They are not intended for use on the Internet. Routers are not supposed to route packets with private source addresses. Nevertheless, some routers do forward packets containing private source addresses.

Additionally, if someone on your ISP's subnet (that is, on your side of the router that you share) is leaking packets with private IP addresses, you'll see them even if the router doesn't forward them. Machines on your own LAN could also leak private addresses if your NAT or proxy configuration is set up incorrectly.

The next three sets of rules disallow incoming packets containing source addresses from any of the Class A, B, or C private network addresses. None of these packets should be seen on a public network:

```
# Refuse packets claiming to be from a Class A private network
$IPT -A INPUT -i $INTERNET -s $CLASS_A -j DROP

# Refuse packets claiming to be from a Class B private network
$IPT -A INPUT -i $INTERNET -s $CLASS_B -j DROP

# Refuse packets claiming to be from a Class C private network
$IPT -A INPUT -i $INTERNET -s $CLASS_C -j DROP
```

The next rule disallows packets with a source address in the loopback network:

```
# Refuse packets claiming to be from the loopback interface
$IPT -A INPUT -i $INTERNET -s $LOOPBACK -j DROP
```

Because loopback addresses are assigned to an internal, local software interface, any packet claiming to be from such an address is intentionally forged.

As with addresses set aside for use in private LANs, routers are not supposed to forward packets originating from the loopback address range. A router cannot forward a packet with a loopback destination address.

The next two rules primarily serve to log matching packets. The firewall's default policy is to deny everything. As such, broadcast addresses are dropped by default and must be explicitly enabled if they are wanted:

```
# Refuse malformed broadcast packets
$IPT -A INPUT -i $INTERNET -s $BROADCAST_DEST -j LOG
$IPT -A INPUT -i $INTERNET -s $BROADCAST_DEST -j DROP

$IPT -A INPUT -i $INTERNET -d $BROADCAST_SRC -j LOG
$IPT -A INPUT -i $INTERNET -d $BROADCAST_SRC -j DROP
```

The first pair of rules logs and denies any packet claiming to come from `255.255.255.255`, the address reserved as the broadcast destination address. A packet will never legitimately originate from address `255.255.255.255`.

The second pair of rules logs and denies any packet directed to destination address `0.0.0.0`, the address reserved as a broadcast source address. Such a packet is not a mistake; it is a specific probe intended to identify a UNIX machine running network software derived from BSD. Because most UNIX operating system network code is derived from BSD, this probe is effectively intended to identify machines running UNIX.

> **CLARIFICATION ON THE MEANING OF IP ADDRESS 0.0.0.0**
> 
> Address `0.0.0.0` is reserved for use as a broadcast source address. The Netfilter convention of specifying a match on any address, any/`0.0.0.0/0`,or `0.0.0.0/0.0.0.0`,doesn't match the broadcast source address. The reason is that a broadcast packet has a bit set in the Layer 2 frame header indicating that it's a broadcast packet destined for all interfaces on the network, rather than a point-to-point, unicast packet destined for a particular destination. Broadcast packets are handled differently than nonbroadcast packets. There is no legitimate nonbroadcast IP address `0.0.0.0`.

The next two rules block two forms of directed broadcasts:

-   # Refuse directed broadcasts
-   # Used to map networks and in Denial of Service attacks
-   $IPT -A INPUT -s $INTERNET -d $SUBNET_BASE -j DROP
-   $IPT -A INPUT -i $INTERNET -d $SUBNET_BROADCAST -j DROP

With the deny-by-default policy and the firewall rules explicitly accepting packets based in part by matching on destination address, neither of these directed broadcast messages will be accepted by the firewall. These rules become more critical in larger setups in which the LAN uses real-world addresses.

With the use of variable-length Network prefixes, a site's network and host fields may or may not fall on a byte boundary. For the sake of simplicity, the `SUBNET_BASE` is your network address, such as `192.168.1.0`. The `SUBNET_BROADCAST` is your network's broadcast address, as in `192.168.1.255`.

Just as with directed broadcast messages, limited broadcasts, confined to your local network segment, are likewise not accepted with the deny-by-default policy and the firewall rules explicitly accepting packets based in part by matching on destination address. Again, the following rule becomes more critical in larger setups in which the LAN uses real-world addresses:

```
# Refuse limited broadcasts
$IPT -A INPUT -i $INTERNET -d $BROADCAST_DEST -j DROP
```

It should be noted that an exception must be made in later chapters for DHCP clients. Broadcast source and destination addresses are used between the DHCP client and server ports initially.

Multicast addresses are legal only as destination addresses. The next rule drops spoofed multicast network packets:

```
# Refuse Class D multicast addresses
# Illegal as a source address
$IPT -A INPUT -i $INTERNET -s $CLASS_D_MULTICAST -j DROP
```

Legitimate multicast packets are always UDP packets. As such, multicast messages are sent point-to-point, just as any other UDP message is. The difference between unicast and multicast packets is the class of destination address used (and the protocol flag carried in the Ethernet header). The next rule denies multicast packets carrying a non-UDP protocol:

```
$IPT -A INPUT -i $INTERNET -p ! udp -d $CLASS_D_MULTICAST -j DROP
```

Multicast functionality is a configurable option when you compile the kernel, and your network interface card can be initialized to recognize multicast addresses. The functionality is enabled by default in the default kernel from many newer distributions of Linux. You might want to enable these addresses if you subscribe to a network conferencing service that provides multicast audio and video broadcasts. (Multicast is also sometimes used on the local network for global resource discovery, such as with DHCP or routing.)

You won't generally see multicast destination addresses unless you've registered yourself as a recipient. Multicast packets are sent to multiple, but specific, targets by prior arrangement. I have seen multicast packets sent out from machines on our ISPs local subnet, however. The default policy drops multicast packets, even if you have registered as a recipient. You have to define a rule to accept the multicast address. The next rule allows incoming multicast packets for the sake of completeness:

```
$IPT -A INPUT -i $INTERNET -p udp -d $CLASS_D_MULTICAST -j ACCEPT
```

Multicast registration and routing is a complicated process managed by its own IP layer-control protocol, the Internet Group Management Protocol (IGMP, protocol 2). For more information on multicast communication, refer to the "Multicast over TCP/IP HOWTO" at http://www.tldp.org/HOWTO/Multicast-HOWTO.html. Additional resources include RFC 1458, "Requirements for Multicast Protocols"; RFC 1112, "Host Extensions for IP Multicasting" (updated by RFC 2236, "Internet Group Management Protocol Version 2"); and RFC 2588, "IP Multicast and Firewalls."
