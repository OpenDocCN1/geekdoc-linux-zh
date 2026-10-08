# CHAPTER 7 | Networks, Firewalls, and More

Stanford University also suggests that its administrators set up the following message for users who are denied access to TCP Wrappers services. The hostname of the server is substituted for %h in the message.

You have attempted to connect to a restricted access server which you have not been authorized to connect to. Unauthorized access to this system is an actionable offense and will be prosecuted to the fullest extent of the law.

It appears that you have attempted to connect from %h and that host does not have permission/authorization to access this server. Your actions have been recorded and are being reported to the system administrators of this system.

You will now be disconnected!

Of course, the wording will be revised per the policies and characteristics of your organization.

# Packet Filtering Firewalls

When Linux is protected with a packet filtering firewall, it is protected with a set of rules defined by the iptables command. This command can be used to check various parts of a network packet using patterns. If the pattern is matched, you can configure iptables command to accept, reject, deny, or even forward that packet. Different sets of rules can be created for bastion hosts in a demilitarized zone (DMZ) as well as private networks before DMZ.

Before exploring the iptables command that filter packets, be aware that the iptables command is frequently used to masquerade the addresses of a private IP network as a public IP address, typically a public IP address on the Internet.

In any iptables rules that forward a packet won't work unless forwarding options in the /proc/directory, typically in the /proc/sys/net/ipv4/ip_forward file. Such options can be configured on a more permanent basis in the /etc/sysctl.conf configuration file.

While the described here refer to Internet Protocol 4 (IPv4) networking, similar commands and options apply to Protocol 6 (IPv6) networking. In most cases, the only differences are the addresses along with the applicable command (ipt6 instead of iptables).

Packet filtering relies on information embedded in the header of each packet. Based on that information, you can create iptables-based rules that redirect the packet. That information can include network hosts, IP addresses, port numbers, and more.

This section serves as a brief introduction to the iptables command. A good firewall can include dozens of commands, which can identify different packets and/or source/destination addresses. The iptables command can also be configured to specify desired actions to take on those packets. Several excellent books are available that can help you customize iptables firewalls in a bit of detail; some references are listed in the back of this book.