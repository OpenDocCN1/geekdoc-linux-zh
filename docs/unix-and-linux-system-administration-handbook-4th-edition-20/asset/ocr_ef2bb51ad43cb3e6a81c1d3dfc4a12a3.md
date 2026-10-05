# IP spoofing

packets appear to come from inside your network. This subteruge can help an intruder's packets evade network scanners and packet filters.

It is perfectly acceptable for a host to use multiple network interfaces for its own traffic without forwarding third-party traffic.

# ICMP redirects

ICMP redirects (see page 467) can maliciously reroute traffic and tamper with your routing tables. Most operating systems listen to ICMP redirects and follow their instructions by default. It would be bad if your traffic were rerouted to a competitor's network for a few hours, especially while backups were running! We recommend that you configure your routers (and hosts acting as routers) to ignore and perhaps log ICMP redirect attempts.

# Source routing

IP's source routing mechanism lets you specify an explicit series of gateways for the packet to transit on the way to its destination. Source routing bypasses the next-hop routing algorithm that normally runs at each gateway to determine how a packet should be forwarded.

Source routing was part of the original IP specification; it was intended to facilitate testing. It can create security problems because packets are filtered according to their origin. If someone cleverly route a packet to make appear to have originated within your network instead of the Internet, it might slip through your firewall. We recommend that you accept nor forward source-routed packets.

# Broadcast pings and other directed broadcasts

Ping packets addressed to a network's broadcast address (instead of a particular host address) are typically delivered to every host on the network. Such packets have been used in denial of service attacks; for example, the so-called Smurf attacks (The "Smurf attacks" Wikipedia article has details.).

Broadcast pings are a form of "directed broadcast" in that they are sent to the broadcast address of a distant network. The default handling of such packets has been gradually changing. For example, versions of Cisco's IOS over 11.x forward directed broadcasts by default, IOS releases since 12.0 do not. It is usually possible to convince your TCP/IP stack to ignore broadcast packets that come from afar, but because this behavior must be set on each interface, the task can be nontrivial at a large size.

# IP spoofing

The source address on an IP packet is normally filled in the kernel's TCP/IP implementation and is the IP address of the host from which the packet was sent. However, if the software creating the packet uses a raw socket, it can fill in any source address it likes. This is called IP spoofing and is usually associated with