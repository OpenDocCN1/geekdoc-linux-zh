
The address is the source address to substitute for the original source address in the packet, presumably the address of the outgoing interface. Source NAT is what NAT is traditionally used for, to allow outgoing connections. Specifying a single translation address performs NAPT, allowing all local, privately addressed hosts to share your site's single, public IP address.

Optionally, a range of source addresses can be specified. Sites that have a block of public addresses would use this range. Outgoing connections from local hosts would be assigned one of the available addresses, with the public address being associated with a particular local host's IP address. Specifying a range of addresses represents what traditional, basic NAT is usually used for, although iptables SNAT is internally implemented as NAPT in both cases.

The final port specification is another option. The range of ports defines the pool of source ports to choose from on the NAT device's outgoing interface.

The ellipsis represents any other packet selectors that are specified. For example, SNAT could be applied only to a select local host or only for TCP connections. Another use might be for VPN, where connections between two sites might be made between two specific source and destination addresses. An alternative with VPN is that connections might be made between specific source and destination ports.

Why might a site add these match selectors to a NAT rule? These selections are—or should be—made on the filter table's INPUT, OUTPUT, and FORWARD chains. In the case of applying NAT to select hosts, the site might be excluding hosts containing sensitive information. The site might contain networked devices such as printers or local wireless devices, and it might not be clear just what kinds of traffic these devices generate. Matching on TCP might be done as an added assurance that UDP traffic is not being exchanged with the Internet or that UDP traffic is passed only through specific application proxies.

## MASQUERADE SOURCE NAT

The general syntax for MASQUERADE is as follows:

```bash
iptables -t nat -A POSTROUTING -o <outgoing interface> ... \
    -j MASQUERADE [--to-ports <port>[-port]]
```

MASQUERADE doesn't have an option to specify a particular source address to use on the NAT device. The source address used is the address of the outgoing interface.

The optional port specification is one source port or a range of source ports to choose from on the NAT device's outgoing interface.

As with SNAT, the ellipsis represents any other packet selectors that are specified. For example, MASQUERADE could be applied to only a select local host.

## Destination NAT

Two forms of destination NAT exist in the iptables nat table, specified as two distinct targets: DNAT and REDIRECT. DNAT is standard destination address translation. REDIRECT is a specialized form of destination NAT that redirects packets to the NAT device's input or loopback interface.

The two targets can be used on either of the nat table's *PREROUTING* or *OUTPUT* chains. Destination address modifications are applied before the routing decision is made to choose the proper interface. Thus, on the *PREROUTING* chain, DNAT and REDIRECT rules are associated with an incoming interface for packets that are to be forwarded through the device or that are addressed to this host's incoming interface. On the *OUTPUT* chain, DNAT and REDIRECT rules refer to locally generated, outgoing packets from the NAT host itself.

### STANDARD DNAT

The general syntax for DNAT is as shown here:

```bash
iptables -t nat -A PREROUTING -i <incoming interface> ... \
-j DNAT --to-destination <address>[-<address>][:<port>-<port>]
```

and

```bash
iptables -t nat -A OUTPUT -o <outgoing interface> ... \
-j DNAT --to-destination <address>[-<address>][:<port>-<port>]
```

The address is the destination address to substitute for the original destination address in the packet, presumably the address of a local server.

Optionally, a range of destination addresses can be specified. Sites that have a pool of public, peer servers would use this range. Incoming connections from remote sites would be assigned to one of the servers. These addresses could be public addresses assigned to the internal machines. For example, a pool of peer servers appears to be a single server to remote hosts. Alternatively, the addresses could be private addresses and the servers wouldn't be directly visible or addressable from the Internet. In the latter case, the site probably doesn't have public addresses to assign to the servers. Remote hosts attempt to connect to the service on the NAT host. The NAT host forwards the connections transparently to the privately addressed internal server.

The final port specification is another option. The port specifies the destination port, or port range, on the target host's incoming interface that the packet should be sent to.

The ellipsis represents any other packet selectors that are specified. For example, *DNAT* could be applied to redirect incoming connections from a specific remote host to an internal host. Another use might be to redirect incoming connections to a particular service port to the actual server running in the local network.

## REDIRECT DESTINATION NAT

The general syntax for REDIRECT is shown here:

```bash
iptables -t nat -A PREROUTING -i <incoming_interface> ... \ 
-j REDIRECT [--to-ports <port>[-port]]
```

and

```bash
iptables -t nat -A OUTPUT -o <outgoing_interface> ... \ 
-j REDIRECT [--to-ports <port>[-port]]
```

Remember, REDIRECT redirects the packet to this host, which is the host performing the REDIRECT.

Packets arriving on the incoming interface are presumably addressed to some other local host. Another alternative could be that the packet is targeted to a particular local service port, and the packet is redirected to a different port on the host transparently.

Locally generated packets, destined for somewhere else, are redirected back to the loopback interface on this host. Again, a packet targeted to a specific remote service might be redirected back to the local machine, perhaps to a caching proxy, for example.

Optionally, a different destination port or port range can be specified. If no port is specified, the packet is delivered to the destination port that the sender defined in the packet.

The ellipsis represents any other packet selectors that are specified. For example, REDIRECT could be applied to redirect incoming connections to a specific service to a server, logger, authenticator, or some kind of inspection software on the local host. The packet could be sent on from this host after some kind of inspection function was performed. Another use might be to redirect outgoing connections to a particular service back to a server or an intermediate service on this host.

## Examples of SNAT and Private LANs

Source NAT is by far the most common form of NAT. Using NAT to give outgoing Internet access to local, privately addressed hosts was the original purpose of NAT. The following sections provide some simple, real-world examples of using the nat table's MASQUERADE and SNAT targets.

### Masquerading LAN Traffic to the Internet

The MASQUERADE version of source NAT is intended for people with dial-up accounts who get a different IP address assigned at each connection. It also is used by people with *always* on connections, but whose ISP assigns them a different IP address on a regular basis.

The simplest example is a PPP connection. These sites often use a single rule to masquerade all outgoing connections from the LAN:

```bash
iptables -t nat -A POSTROUTING -o ppp0 -j MASQUERADE
```

Masquerading—and NAT in general—is set up with the first packet. With masquerading, a single nat rule can be sufficient. The NAT and connection state tracking take care of the incoming packets. The FORWARD rule pair is necessary, though, as in this example:

```bash
iptables -A FORWARD -o ppp0 \
-m state --state NEW,ESTABLISHED,RELATED -j ACCEPT
```

```bash
iptables -A FORWARD -o <LAN interface> \
-m state --state ESTABLISHED,RELATED -j ACCEPT
```

In this simple type of setup, the incoming interface doesn’t need to be specified. FORWARD rules refer to traffic crossing between interfaces. If the host has a single network interface and a single ppp interface, anything forwarded out one interface must necessarily originate from the other interface. Anything accepted by the FORWARD rules in the filter table during routing will be masqueraded by the POSTROUTING rule in the nat table.

Even with short-term phone connections, the single FORWARD rule allowing outgoing NEW connections should be broken out into rules for specific services. Depending on the networked devices in the LAN and how they operate, you most likely want to limit what LAN traffic gets forwarded.

Here’s an example of a single FORWARD rule pair:

```bash
iptables -A FORWARD -i <LAN interface> -o ppp0 \
-m state --state NEW,ESTABLISHED,RELATED -j ACCEPT
```

```bash
iptables -A FORWARD -i ppp0 -o <LAN interface> \
-m state --state ESTABLISHED,RELATED -j ACCEPT
```

In this example, the single FORWARD rule pair is broken out into several more specific rules allowing only DNS queries and standard web access. Other LAN traffic isn’t forwarded, as shown by these commands:

```bash
iptables -A FORWARD -i ppp0 -o <LAN interface> \
-m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A FORWARD -o ppp0 \
-m state --state RELATED,ESTABLISHED -j ACCEPT
```

```bash
iptables -A FORWARD -o ppp0 -p udp \
--sport 1024:65535 -d <name servers> --dport 53 \
-m state --state NEW -j ACCEPT
```
