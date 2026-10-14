| Command | Description | Example |
|---|---|---|
| route | Displays the kernel's routing table or modifies that table by adding or removing a network route | route add -net 192.168.100.0 netmask 255.255.255.0 dev eth0 |
| routed | Daemon for basic network routing using the RIP protocol | routed |

# Key Terms

/etc/dhcpd.conf — Configuration file used to define the operation of the DHCP server daemon, dhcpd.
/etc/host.conf — Configuration file that specifies the order in which the resolver should consult resources to resolve the host name to an IP address. Not used in many Linux systems because /etc/nsswitch.conf is used instead.
/etc/hosts — Configuration file that stores IP addresses and corresponding domain names for hosts, usually those frequently accessed on a local network.
/etc/printcap — Configuration file that defines print queues, specifically used for the LPRng printing system.
/etc/resolv.conf — Configuration file that configures the Linux resolver by listing the computer's domain and the IP address of one or more DNS name servers.
Address Resolution Protocol (ARP) — A protocol that broadcasts a message to an entire network segment in order to obtain a host's MAC address, or, if the MAC address is known, to obtain a host's IP address.
alternatives printing system — A method used in Red Hat Linux and Fedora to permit both LPRng and CUPS printing systems to reside on the same Linux system using symbolic links for commonly used printing commands.
ARP cache — A list of IP address-to-hardware mappings maintained by the ARP protocol to assist in routing packets. Viewed using the arp command.
BOOTP — A protocol used by diskless computers to obtain configuration information. Rarely used now, but similar to DHCP, which is backwards compatible with BOOTP.
Border Gateway Protocol (BGP) — A widely used external routing protocol.
broadcast address — An IP address that a computer on a network can use to send a packet to all computers on that network.
Common UNIX Printing System (CUPS) — A printing system that permits browser-based configuration and print management. Intended to eventually replace the LPRng printing system.
dynamic routing — Collecting and updating routing table information automatically using a routing protocol such as RIP, OSPF, or BGP.
exterior routing protocols — Routing protocols designed for routing packets between networks controlled by different organizations; packets are routed based on administrative policies, often controlled by how much a particular organization's routing information is trusted.