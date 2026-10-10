and type the port number and select the protocol you want to enable. Click OK when you are done.

+   - **Trusted Interfaces** — You can identify any of your network interfaces as being trusted. No incoming ports are blocked from requests from a trusted interface. You should never assign an external interface to a public network to be trusted. However, you might have a dedicated network connection or a connection to a small local LAN that you want to be trusted.

+   - **Masquerading** — By identifying an interface as a masquerading interface, you can allow other computers on your LAN with private IP addresses to use your computer as a router to the Internet (or other network). This presumes that your Fedora system has another network interface with a route to the Internet. By selecting at least one network interface as providing IP masquerading, packet forwarding support is automatically turned on. (See descriptions of masquerading later in this chapter.)

+   - **Port Forwarding** — You indicate that traffic directed to a specific port on the local interface be redirected to either another local port or to a port on another computer. This is one way to allow a server behind the firewall to provide public Web, SSH, FTP, or other service.

+   - **ICMP** — Allow or disallow Internet Control Message Protocol (ICMP) error messages to be sent between networked computers. For example, a ping request is often used to check if a computer on the network is up and running. Ping requests can also be used for denial-of-service attacks. By default, all ICMP packets are allowed.

+   - **Custom Rules** — Creating custom rules can be a bit trickier than simply opening access for a port. You can create an iptables rule in a separate file (in iptables-save format as described later in this chapter) and assign that rule to a filter, NAT, or mangle iptables table. Click Add and indicate the address type (ipv4 or ipv6), type of table, and file containing the rule. Click OK to add the rule.

Before clicking Apply to save your settings, consider that doing so will overwrite your existing firewall rules. If you have done any hand editing of the configuration file (/etc/sysconfig/iptables or /etc/sysconfig/ip6tables for the IPv6 firewall), those changes will be overwritten. Make a backup copy of these files before continuing.

Configuring iptables to set up logging, port forwarding, network address translation, and other features can be done manually, as described in the next sections.

# Configuring an iptables firewall

The remaining sections on iptables in this chapter describe a more manual way of working with your iptables firewall in Linux. I also cover how to implement special iptables features that are not available from the Firewall Configuration window (such as NAT).