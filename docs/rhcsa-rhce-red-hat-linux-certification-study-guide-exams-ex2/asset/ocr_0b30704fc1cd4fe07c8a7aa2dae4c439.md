As an example, let’s define the range of addresses for a private network. Start with the private network address 192.168.122.0. Use the standard subnet mask for a class C network, 255.255.255.0. Based on these two addresses, the broadcast address is 192.168.122.255, and the range of IP addresses that you can assign on that particular network is 192.168.122.1 through 192.168.122.254. That subnet mask is also defined by the number of associated bits, 24. In other works, the given network can be represented by 192.168.122.0/24. That’s also known as Classless Inter-Domain Routing (CIDR) notation.

IPv6 networks use a similar concept for netmasks, which are always expressed in CIDR notation. For example, even point-to-point networks have a netmask of /64. That allows 64 bits to be used for the 48-bit hardware address. Remaining addresses can be allocated to specific network cards.

The standard IPv6 network has a /48-bit netmask. That supports the configuration of 16 bit subnets. The remaining 64 bits are still used in part for network cards, as described previously for point-to-point networks.

Related to networking and netmasks is the concept of the gateway. It’s an IP address that defines the junction between the local network and an external network. While that gateway IP address is part of the local network, it’s attached to a system or a router with an IP address on a different network such as the public Internet. The gateway IP address is normally configured in the routing table for the local system, as defined by the route or netstat -r command described in the following section.

If this is confusing to you in any way, please refer to the IP Sub-Networking Mini-HOWTO and the Linux IPv6 HOWTO of the Linux Documentation Project at www.tldp.org.

# Tools, Commands, and Gateways

There are a substantial number of tools available to manage the TCP/IP protocol suite on your Linux computer. Four of the more important network management commands are ping, ifconfig, arp, netstat -r, and route. There’s also an IPv6-specific version of the ping command, ping6. The dhclient command is frequently used to automate the configuration that can be done with some of these commands.

But these are just the commands. In the next section, you’ll examine the Red Hat files that determine the commands that are called upon to configure networks automatically during the boot process. Such commands are governed by the main network configuration service script, /etc/init.d/network. They can also be manually called with commands such as ifup and ifdown.