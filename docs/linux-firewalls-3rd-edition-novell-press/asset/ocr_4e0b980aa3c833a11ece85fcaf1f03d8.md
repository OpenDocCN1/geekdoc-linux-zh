The first pair of rules logs and denies any packet claiming to come from `255.255.255.255`, the address reserved as the broadcast destination address. A packet will never legitimately originate from address `255.255.255.255`.

The second pair of rules logs and denies any packet directed to destination address `0.0.0.0`, the address reserved as a broadcast source address. Such a packet is not a mistake; it is a specific probe intended to identify a UNIX machine running network software derived from BSD. Because most UNIX operating system network code is derived from BSD, this probe is effectively intended to identify machines running UNIX.

> **CLARIFICATION ON THE MEANING OF IP ADDRESS 0.0.0.0**
> 
> Address `0.0.0.0` is reserved for use as a broadcast source address. The Netfilter convention of specifying a match on any address, any/`0.0.0.0/0`,or `0.0.0.0/0.0.0.0`,doesn't match the broadcast source address. The reason is that a broadcast packet has a bit set in the Layer 2 frame header indicating that it's a broadcast packet destined for all interfaces on the network, rather than a point-to-point, unicast packet destined for a particular destination. Broadcast packets are handled differently than nonbroadcast packets. There is no legitimate nonbroadcast IP address `0.0.0.0`.

The next two rules block two forms of directed broadcasts:

+   # Refuse directed broadcasts
+   # Used to map networks and in Denial of Service attacks
+   $IPT -A INPUT -s $INTERNET -d $SUBNET_BASE -j DROP
+   $IPT -A INPUT -i $INTERNET -d $SUBNET_BROADCAST -j DROP

With the deny-by-default policy and the firewall rules explicitly accepting packets based in part by matching on destination address, neither of these directed broadcast messages will be accepted by the firewall. These rules become more critical in larger setups in which the LAN uses real-world addresses.

With the use of variable-length Network prefixes, a site's network and host fields may or may not fall on a byte boundary. For the sake of simplicity, the `SUBNET_BASE` is your network address, such as `192.168.1.0`. The `SUBNET_BROADCAST` is your network's broadcast address, as in `192.168.1.255`.

Just as with directed broadcast messages, limited broadcasts, confined to your local network segment, are likewise not accepted with the deny-by-default policy and the firewall rules explicitly accepting packets based in part by matching on destination address. Again, the following rule becomes more critical in larger setups in which the LAN uses real-world addresses: