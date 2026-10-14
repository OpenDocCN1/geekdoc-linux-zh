Red Hat 6.x, for example, keeps its basic interface configuration in /etc/sysconfig/network-scripts. For the configuration of the interface eth0, the file with all of the values is ifcfg-eth0. At boot time, the script /etc/rc.d/init.d/network finds all the interfaces and attempts to run script ifup interface on the ifcfg-devname script (which in turn runs some other scripts).

> NOTE
> The networks 10.0.0.0 and 192.168.69.0 are reserved for private networks. Anyone may use them for their own network (corporations often use them for network numbers behind a firewall), but no router on the true Internet knows about them. IANA also reserves names example.com and example.net for use in examples (such as those in this book).

# The route Command

To do anything useful, network packets need a route to travel along. The route command (route {add|del} args ...) changes the routes that your computer knows, or the routing table. (Routing is a complex subject, so it's best to keep the table as simple as possible when you're starting with a small network.)

With no arguments, route returns the current routing table. The -n option turns off host name resolution and comes in particularly handy, since you usually want to look at the table when there is some sort of problem (if you have trouble with the network, the DNS server is probably having trouble as well).

# Setting the Default Route

If a network packet doesn't have a specific route to follow in the kernel routing table, it goes to the default route (also known as the default gateway or gateway). If no default route exists and nothing in the routing table applies to a packet, the program trying to send the packet gets a "No route to host" error. Use

```
# route add default gw 10.0.0.1
```

to set the default route to 10.0.0.1.

# Adding a Route

To add a route, use the command

```
# route add -net 10.0.1.0 netmask 255.255.255.0 gw 10.0.0.48
```

This adds a route to the network 10.0.1.0, with netmask 255.255.255.0 and gateway 10.0.0.48. (As explained in Section 2.4, this network consists of the hosts from 10.0.1.1 to 10.0.1.254.)

# Showing the Kernel Routing Table

The command route -n (or netstat -nr) shows the kernel routing table. The -n option disables domain name resolution. If you're running this command,