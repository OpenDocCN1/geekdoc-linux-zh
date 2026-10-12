Some Linux network drivers use a technique called copy and checksum to optimize host performance. However, for a machine that acts as a router most of the time and is forwarding most packets to another host, such optimization is not needed—select the default.

**IP: tunneling (CONFIG_NET_IPIP) [N/y/m/?]**

Tunneling means encapsulating data of one protocol within another protocol and sending it over a channel that understands the encapsulating protocol. This particular tunneling driver implements encapsulation of IP within IP, which sounds kind of pointless but can be useful if you want to make your (or some other) machine appear on a different network from the one it is physically connected to or to use mobile-IP facilities (allowing laptops to seamlessly move between networks without having to change their IP addresses).

**IP: GRE tunnels over IP (CONFIG_NET_IPGRE) [N/y/m/?] ?**

GRE (Generic Routing Encapsulation) allows encapsulating of IPv4 or IPv6 over the existing IPv4 infrastructure.

**IP: aliasing support (CONFIG_IP_ALIAS) [N/y/?]**

If you want to attach multiple IP addresses to a single network interface, say yes here.

(*.*

**IP: TCP syncookie support (not enabled per default) (CONFIG_FX_SYN_COOKIES) [N/y/?]**

Normal TCP/IP networking is open to an attack known as “SYN flooding.” This denial-of-service attack prevents legitimate remote users from connecting to your computer during an ongoing attack and requires very little work from the attacker, who can operate from anywhere on the Internet. SYN cookies provide protection against this type of attack. If you choose y here, the TCP/IP stack uses a cryptographic challenge protocol known as “SYN cookies” to enable legitimate users to continue to connect even when your machine is under attack. There is no need for legitimate users to change their TCP/IP software, but SYN cookies may prevent correct error reporting on clients when the server is overloaded. If this happens frequently, you had better turn them off. If you choose y here, note that choosing the default does not enable SYN cookies; you can enable