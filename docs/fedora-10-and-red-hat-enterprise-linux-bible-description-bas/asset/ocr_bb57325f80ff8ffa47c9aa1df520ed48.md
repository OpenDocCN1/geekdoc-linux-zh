dedicated network connection or a connection to a small local LAN that you want to be trusted.

+   - Masquerading — By identifying a Masquerading interface, you can allow other computers on your LAN with IP addresses to use your computer as a router to the Internet (or other network). This presumes that your Fedora system has another network interface with a route to the Internet. By selecting at least one network interface as IP Masquerading, packet forwarding is automatically turned on. (See details of Masquerading later in this chapter.)

+   - Port Forwarding — You indicate that directed to a specific port on the local interface be redirected to another local port or to port on another computer. This is one way to allow a server behind the firewall to protect public Web, SSH, FTP or other service.

+   - ICMP — Allow or deny Internet Control Message Protocol (ICMP) error messages to be sent between networked computers. For example, a ping request is often used to check if a computer on the network is up and running.

+   - Custom Rules — Creating custom rules can be a bit tricky than simply opening access for a port. You can create an iptables rule in a separate file (in iptables-save format as described later in this chapter) and assign that rule to a filter, NAT, or mangle iptables table. Click Add and identify the address type (ipv4 or ipv6), type of table, and containing the rule. Click OK to add the rule.

Before applying to your settings, consider that doing so will overwrite your existing firewall rules. If you have done any editing of the configuration file (/etc/sysconfig/iptables), those changes will be overwritten. Make a backup copy of that file before continuing.

Configuring iptables to set up logging, port forwarding, network address translation, and other features can be done manually, as described in the sections.

# Configuring iptables firewall

The remaining sections on iptables in this chapter describe a manual way of working with your iptables firewall in Linux. I also cover how to implement special iptables features that are not available from the Firewall Configuration window (such as port forwarding and NAT).

# Turning on iptables

The iptables feature (also referred to as netfilter) is the default firewall software when you install Fedora or RHEL.

This section describes how to turn on iptables and set up firewall rules for different types of situations. It also tells how to turn on features related to firewalls that allow you