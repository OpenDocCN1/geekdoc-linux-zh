The first of these commands adds a route for local traffic—anything addressed to the 192.168.203.0 network goes out over the appropriate NIC. This command is usually not required because the ifconfig command usually does this job. The low–level TCP/IP protocols include routines that allow a computer to locate any other computer that's connected to its local network segment. The second command takes over when packets are destined for an address other than the 192.168.203.0 network (or any other network defined by an explicit route). In this case, the system directs the packets to 192.168.203.1, which should be a router capable of passing the packets on to the appropriate destination. (In fact, it may pass them on to another router, and so on for quite a few hops on the network.)

Note  If you're configuring systems on a local network that will not be connected to the Internet, there's no need to specify a gateway route.

You can examine your routing table by issuing the route command without any options (or with the –n option, if you want to see IP addresses rather than machine names). For instance:

```
# route –n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref  Use Iface
192.168.203.0   0.0.0.0       255.255.255.0   U     0      0      0     eth0
127.0.0.0       0.0.0.0       255.0.0.0       U     0      0      0     lo
0.0.0.0         192.168.203.1 0.0.0.0         UG    0      0      0     eth0
```

This output reveals three routes: one for the 192.168.203.0 network, one for the localhost interface (which is actually configured as an entire network), and one for the default route. Most desktop and even server systems will have routing tables that resemble this one. If a computer has multiple NICs, or if its network is unusually complex in any of several ways, the routing table may have additional entries.

Most Linux systems include calls to route in startup scripts. In Red Hat 7.3, /etc/rc.d/init.d/network is responsible for starting networking, including setting the route, but it calls several others to do the work. You can therefore modify this file, use Webmin to do the job, or add calls to route to some other startup script, such as /etc/rc.d/rc.local.

# ## Specifying DNS Servers

In order to resolve hostnames into IP addresses for arbitrary systems on the Internet, Linux must know the IP address of at least one DNS server. Linux stores this information in the /etc/resolv.conf file, along with information on its own default domain name. A typical /etc/resolv.conf file looks like this:

```
domain room1.threeroomco.com
search room2.threeroomco.com room3.threeroomco.com
nameserver 192.168.203.1
nameserver 192.168.203.20
```

There are three important keywords used in this file:

+   - **domain** This specifies the domain to which the system belongs. Linux tries to resolve names using the specified domain first. For example, if you use the machine name ginkgo and the above /etc/resolv.conf file, Linux first searches for a computer called ginkgo.room1.threeroomco.com. This feature allows you to omit the domain name portion of a machine name when a target computer is in the same domain as the source machine.