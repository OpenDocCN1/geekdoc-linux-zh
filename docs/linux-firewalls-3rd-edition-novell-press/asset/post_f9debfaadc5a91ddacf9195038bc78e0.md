
In the case of a very small personal or business home site, one possibility is to run a public server on the gateway machine. (Hosting a public web server on the firewall host would otherwise be considered a dangerous idea.) Possibly, a second, private proxy web server runs on an internal machine. In this situation, the public server may or may not offer SSL service. The internal web server offers proxy service. The private server isn’t accessible from the gateway machine.

The proxy server in this example could run in the LAN, but there wouldn’t be an “example” because the firewall rules on both the gateway and the choke would remain the same as in the first web section. Placing the proxy web server in the DMZ or on the choke host demonstrates the difference between the client-side rules and the server-side rules.

From the gateway’s perspective, the internal web proxy appears to be a web client initiating connections to remote servers. This example requires a constant of `DMZ_WWW_PROXY`:

```
$IPT -A FORWARD -i $DMZ_INTERFACE -o $EXTERNAL_INTERFACE -p tcp \ -s $DMZ_WWW_PROXY --sport $UNPRIVPORTS --dport 80 \ -m state --state NEW -j ACCEPT
```

```
$IPT -A FORWARD -i $DMZ_INTERFACE -o $EXTERNAL_INTERFACE -p tcp \ -s $DMZ_WWW_PROXY --sport $UNPRIVPORTS --dport 443 \ -m state --state NEW -j ACCEPT
```

The choke’s rules must account for the port that the web proxy is bound to, thus the `WEB_PROXY_PORT` constant in this example. From the choke’s perspective, the local web proxy appears to be a server running on a port other than TCP port 80, as these rules show:

```
$IPT -A FORWARD -i $LAN_INTERFACE -o $DMZ_INTERFACE -p tcp \ -s $LAN_ADDRESSES --sport $UNPRIVPORTS \ -d $DMZ_WWW_PROXY --dport $WEB_PROXY_PORT \ -m state --state NEW -j ACCEPT
```

```
$IPT -A OUTPUT -o $DMZ_INTERFACE -p tcp \ -s $DMZ_IPADDR --sport $UNPRIVPORTS \ -d $DMZ_WWW_PROXY --dport $WEB_PROXY_PORT \ -m state --state NEW -j ACCEPT
```

## Choke as a Local DHCP Server (UDP Ports 67 and 68)

DHCP provides network configuration information to hosts. We often think of DHCP mostly in terms of assigning IP addresses, but it also can provide information such as your network mask and MTU, the address of the first-hop router, name server addresses, and the domain name.

Although you should never send DHCP server messages to the Internet (with the notable exception of your gateway that might need to contact your ISP's DHCP server), some people run a private DHCP server to assign IP addresses to local machines. DHCP can be useful not only for assigning IP addresses on a larger LAN with many machines, but also for very small personal home LANs. In fact, some people with a single standalone system sometimes run the DHCPD server locally if they carry a laptop computer between home and work. If the work environment assigns IP addresses dynamically, using DHCP at home makes transporting the laptop between networks easier. Additionally, some networked printers and wireless devices can or do use DHCP to discover their IP address when they come online.

For this example, the *chcpd* server is running on the choke machine, providing dynamic IP address assignment for machines on the private LAN:

```
$IPT -A INPUT -i $LAN_INTERFACE -p udp \
-s $BROADCAST_SRC --sport 68 \
-d $BROADCAST_DEST --dport 67 -j ACCEPT
```

```
$IPT -A OUTPUT -o $LAN_INTERFACE -p udp \
-s $BROADCAST_SRC --sport 67 \
-d $BROADCAST_DEST --dport 68 -j ACCEPT
```

```
$IPT -A OUTPUT -o $LAN_INTERFACE -p udp \
-s $LAN_IPADDR --sport 67 \
-d $BROADCAST_DEST --dport 68 -j ACCEPT
```

```
$IPT -A INPUT -i $LAN_INTERFACE -p udp \
-s $BROADCAST_SRC --sport 68 \
-d $LAN_IPADDR --dport 67 -j ACCEPT
```

```
$IPT -A OUTPUT -o $LAN_INTERFACE -p udp \
-s $LAN_IPADDR --sport 67 \
-d $LAN_ADDRESSES --dport 68 -j ACCEPT
```

```
$IPT -A OUTPUT -o $LAN_INTERFACE -p udp \
-s $LAN_IPADDR --sport 67 \
-d $LAN_ADDRESSES --dport 68 -j ACCEPT
```

```
$IPT -A INPUT -i $LAN_INTERFACE -p udp \
-s $LAN_ADDRESSES --sport 68 \
-d $LAN_IPADDR --dport 67 -j ACCEPT
```

CHAPTER 6: Packet Forwarding

## Logging

Logging dropped packets on the internal interfaces is a good idea, even if the LAN is a relatively trusted environment. Logging is a major tool when debugging firewall problems and understanding communication protocols, both in cases in which different vendors have not strictly adhered to the protocol standards and in cases in which you don't know just what the protocol is. Application protocol information is often difficult to find or is incomplete because network-application writers usually are thinking in terms of an unfiltered, open network. If all traffic were allowed between the private LAN and the choke machine, logging still might be enabled on a port-specific basis or for broadcast traffic. However, although allowing all local traffic is easier in the short term for trusted environments, it can make debugging more difficult when packets are then dropped by the forwarding rules or by the gateway's firewall rules.

## Converting the Gateway from Local Services to Forwarding

The gateway firewall from Chapter 4 needs some further adjustments to its rules. The services that had been hosted on the gateway have moved to the DMZ. This chapter has shown the forwarding rules on at least one of the two firewalls when the rules were the same, and on both firewalls when the respective rules were a bit different. I don't want to be unnecessarily repetitive and belabor the rules on the gateway.

In the interests of space and patience, yours and mine, the modified prelude to the example from Chapter 4 is not presented here. The modifications are simply to convert the *error-checking* rules from the local *INPUT* and *OUTPUT* chains to the *FORWARD* chain because the local services are moving into the DMZ. Both examples, from Chapter 4 and from this chapter, are presented in their entirety, without interspersed text, in Appendix B, “Firewall Examples and Support Scripts.”

## Summary

This chapter covered some of the firewall options available when you're protecting a LAN. Security policies are defined relative to the site's level of security needs, the importance of the data being protected, and the cost of lost data or privacy. Starting with the bastion firewall developed in Chapter 4 as the basis, LAN and firewall setup options were discussed in increasingly complex configurations.

The major emphasis in this chapter was to use the firewall example from Chapter 4 as the basis to develop a formal, elaborate, textbook type of firewall. The bastion became a forwarding gateway firewall with two network interfaces: one connected to the Internet and one connected to a perimeter network, or DMZ. Public Internet services were offered from machines in the DMZ network. A second firewall, a choke firewall, was also connected to the DMZ network, separating the internal, private LAN from the quasi-public server machines in the perimeter network. Private machines were protected behind the choke firewall on the internal LAN. The choke firewall protected any other machine in the perimeter network.

Some services, such as IRC or RealAudio, do not lend themselves to packet filtering because of their application communication protocols, such as requiring incoming connections from the server or multiple client/server exchanges over both TCP and UDP. These types of services require additional help from application-level proxies.

# CHAPTER 7

## NAT—Network Address Translation

Network Address Translation is a technology to substitute one source or destination address in the IP header with another address. Traditionally, it's an IP address translation technology to map packets between two different addressing realms. NAT's most common use is to map outgoing connections between a privately addressed local network and the publicly addressable Internet. In fact, that was what it was originally proposed to do, primarily in conjunction with the then newly defined private class address spaces; both were attempts to alleviate the IPv4 address space shortage.

This chapter introduces the concept of NAT and tells what the various types of NAT are typically used for.

## The Conceptual Background of NAT

NAT was first presented in 1994 in RFC 1631, which was later replaced by RFC 3022. NAT was proposed as a possible short-term, temporary solution (to be used until IPv6 was deployed) to the growing shortage of public IP addresses. NAT also was seen as a possible solution to the growing demands on routers that handled noncontiguous address blocks. It was thought that NAT might possibly reduce or eliminate the need for CIDR, which, in turn, was prompting address reallocations and changes to router software and network configurations. NAT was also seen as a means to avoid the cost and overhead of local network renumbering when the address spaces were re-allocated, or when a site changed service providers and was assigned a new public address block.
