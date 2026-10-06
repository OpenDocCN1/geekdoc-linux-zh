# Chapter 23: Setting Up a DHCP Boot Server 911

# Opening your firewall and SELinux for DHCP

The firewall on your DHCP server must be configured to allow access to UDP ports 67 and 68. The easiest way to do this is to select System -> Administration -> Firewall from the GNOME desktop. From the Firewall Configuration window that appears select Other Ports and add UDP ports 67 and 68.

If you prefer to use iptables directly to change your firewall, you can add a new rule to iptables and then save the changes. Type the following as root:

```
# iptables -I INPUT -i eth0 -p udp --sport 67:68 --dport 67:68 -j ACCEPT
```

In this example, requests are allowed from source and destination ports 67 and 68 (--sport 67:68 and --dport 67:68)) on the eth0 interface (which is your first Ethernet card). DHCP uses the UDP protocol (-p udp). If your DHCP server is also a routing firewall for your network, you want to make sure that you are only offering DHCP services to your LAN and not to the Internet (You may need to figure out if eth0, eth1, or some other card is connected to your LAN.)

If the rule was added (type iptables -L -n to make sure), you can save your firewall configuration so that the new rule is included permanently. To change your firewall, type the following (as root user):

```
# service iptables save
```

This updates your /etc/sysconfig/iptables file so that all the current rules (including the one you just added) are included the next time iptables is restarted. To restore your firewall settings without rebooting, use the iptables-restore command:

```
# iptables-restore < /etc/sysconfig/iptables
```

SELinux should not block normal operations of the dhcpd daemon. If it does, however, you can consider SELinux to permissive by setting setforce 0 on the command line as root user.

# Configuring the /etc/dhcpd.conf file

Suppose you have a pool of IP addresses that you want to distribute to a set of computers that are all on the same subnet. In other words, all the computers are connected to one switch or switches with no routing between the devices. Here is an example of a simple dhcpd.conf file:

```
ddns-update-style interim;
ignore client-updates;

subnet 10.0.0.0 netmask 255.255.255.0 {
  option routers 10.0.0.1;
  option domain-name-servers 10.0.0.1;
```