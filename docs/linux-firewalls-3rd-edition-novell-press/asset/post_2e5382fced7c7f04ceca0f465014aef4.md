
For an added twist, you may have your VPN server set up to accept dial-in connections so that you do not have to go through the Internet at all.

The point to make with this example is that you, the user, must do something such as start a program on the laptop to initiate a VPN connection. If it's a Linux-based laptop, you may need to start IPsec services using a script after you are connected to the Internet.

## Connecting Networks

Let’s contrast the preceding case with the case in which you want to connect two networks. These networks could be in separate physical locations, or they could just be two separate subnets of the same network.

In this configuration, the VPN gateways have startup scripts to start IPsec services at boot time. The servers establish a secure connection with each other. Both gateways have a static route to the other gateway. From a user perspective, they don’t need to do anything to communicate and share information between networks. All communication is taken care of by the VPN gateways. From the perspective of the user, it looks as though Network 2 is on the same network as Network 1. This may be a slight oversimplification, of course, but that is essentially what happens.

> **AUTHENTICATION**
>
> It’s important to note that, in both of these configurations, the user is not being authenticated. Instead, the computer that the VPN software is running on is authenticated. This is particularly noticeable in the dual-network configuration. Here the gateways know about each other and authenticate traffic coming from the other. This process differs greatly from the traditional client/server thinking and technology we have today.

You can set up a lot more complex configurations than those shown here. However, they all have similarities. All VPN gateways know about and have routes to the other VPN gateways in any configuration. Authentication occurs at the gateway level, not the user level.

## VPN and Firewalls

A VPN can be placed in front of a firewall, be placed behind a firewall, or be part of a firewall implementation. Placing the VPN in front of a firewall is not very common. It is more common to use a firewall/VPN combo or to put the VPN behind the firewall itself.

Combining a VPN system and a firewall is one of the more flexible solutions. It also requires less hardware and thus unfortunately also gives a single point of failure. However, it should be stressed that the best solution is to have a VPN behind the firewall or as part of a DMZ configuration. A separate firewall and VPN is set up because it is more secure. If a potential attacker managed to break your firewall/VPN, your network and also your remote networks could potentially be compromised. You want to avoid this problem and make it as hard for the attacker as possible.

If your firewall also performs NAT, you may run into some troubles with some VPN configurations. In particular, your firewall must be set up to route packets based on the protocol (GRE, AH, ESP) instead of on the port alone.

A NAT/firewall is incompatible with the AH protocol regardless of the mode (transport or tunnel). IPsec VPNs using AH digitally sign the outbound packet, both data payload and headers, with a hash value appended to the packet. AH doesn't encrypt the packet contents (data payload). If a NAT/firewall is between the IPsec endpoints, it rewrites either the source address or the destination address with one of its own (depending on the NAT setup). The VPN at the receiving end tries to verify the integrity of the inbound packet by computing its own hash value and complains that the hash value appended to the packet doesn't match. The VPN, unaware of the NAT/firewall in the middle, thinks that the packet has been altered.

You can use ESP with ESP in tunnel mode with authentication. ESP in tunnel mode encapsulates the entire original packet (including headers) in a new IP packet. The new packet's source address is the outbound address of the sending VPN gateway, and its destination address is the inbound address of the VPN at the receiving end. When using ESP in tunnel mode with authentication, the packet contents are encrypted. The encrypted contents (the original packet), not the new headers, are signed with a hash value appended to the packet.

Integrity checks are performed over the combination of the original header plus the original payload. If you're using ESP in tunnel mode with authentication, these are not changed by the NAT/firewall.

A NAT/firewall may interfere with IPsec (both AH and ESP) if it prevents the two VPN gateways from successfully negotiating security associations using ISAKMP/IKE with X.509 certificates. If the two VPN gateways exchange signed certificates that bind each gateway's identity to its IP address, NAT address rewriting will cause the IKE negotiation to fail.

It is for this reason that combined VPN and firewall configurations are becoming so popular. Rules to manage this situation can be set up and maintained easily.

## Summary

Virtual private networks are popular because they leverage existing infrastructure to provide a seamless network experience to end users. Numerous implementations of VPNs are available, taking advantage of the different protocols available for creating VPNs. As you would expect, Linux has several options available, including Openswan and PoPToP, among others.

Some problems exist when connecting VPNs through NAT-enabled firewalls. This is because IPSec creates a digital signature based on the IP header, which is altered during the NAT process.

# APPENDIX D

## Glossary

This glossary defines terms and acronyms used in the book. Multiword terms are alphabetized on the major noun in the term, followed by a comma and the rest of the term.

- **ACCEPT**: A firewall-filtering rule decision to pass a packet through to its next destination.
- **accept-everything-by-default policy**: A policy that accepts all packets that don't match a firewall rule in the chain. Therefore, most firewall rules are DENY rules defining the exceptions to the default accept policy.
- **ACK**: The TCP flag that acknowledges receipt of a previously received TCP segment.
- **application-level gateway**: *See also* proxy, application-level. Often referred to as ALG, an application-level (or layer) gateway is an overloaded term. In firewall terms, ALG often refers to application-specific support modules that inspect application payload for embedded addresses and ports, and that recognize secondary streams associated with the session.
- **AUTH**: TCP service port 113, associated with the **ident** user authentication server.
- **authentication**: The process of determining that an entity is who or what it claims to be.
- **authorization**: The process of determining what services and resources an entity can use.
- **bastion**: *See* firewall, bastion.
- **BIND**: Berkeley Internet Name Domain, the Berkeley implementation of the DNS protocol.
- **BOOTP**: Bootstrap Protocol, which is used by diskless workstations to discover their IP address and the location of the boot server, and to initiate the system download over TFTP before booting. BOOTP was developed to replace RARP.
- **BOOTPC**: UDP service port 68, associated with the BOOTP and DHCP clients.
- **bootpd**: The BOOTP server program.
- **BOOTPS**: UDP service port 67, associated with the BOOTP and DHCP servers.
- **border router**: A device to route packets that resides on the edge or boundary of a network.
- **broadcast**: An IP packet that is addressed and sent to all interfaces connected to the same network or subnet.
- **CERT**: Computer Emergency Response Team, an information coordination center and Internet security emergency prevention center formed at the Software Engineering Institute of Carnegie Mellon University after the Internet Worm incident in 1988.
- **CGI**: Common Gateway Interface. CGI programs are local programs executed by the web server on behalf of the remote client. CGI programs are often Perl scripts, so these programs are often called CGI scripts.
- **chain**: The list of rules defining which packets can come in and which can go out through a network interface.
- **checksum**: A number produced by performing some arithmetic computation on the numeric value of each byte in a file or packet. If the file is changed, or the packet corrupted, a second checksum produced for the same object will not match the original checksum.
- **choke**: See firewall, choke.
- **chroot**: Both a program and a system call that defines a directory to be the root of the filesystem, and that then executes a program to run confined to that virtual filesystem.
- **circuit gateway**: See proxy; circuit-level.
- **class, network address**: Historically, one of five classes of network addresses. An IPv4 address is a 32-bit value. The network space is divided into Class A through Class E addresses, depending on the value of the first 4 most significant bits in the 32-bit value. The Class A network address space maps 128 separate networks, each addressing more than 16 million hosts. The Class B network address space maps 16,384 networks, each addressing up to 64,534 hosts. The Class C network address space maps about 2 million networks, each addressing up to 254 hosts. Class D is used for multicast addresses. Class E is reserved for unspecified or experimental purposes. The network classes have largely become an artifact with the
