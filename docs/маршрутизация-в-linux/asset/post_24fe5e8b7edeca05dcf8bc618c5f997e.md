
**-n**

The -n option turns off name resolution so that all the entries printed with the route command are printed using IP addresses rather than host names.

**-v**

The -v option was originally used with the route command to provide additional information—most notably the netmask of the route entry, however, current versions of the route command provide the additional information without the -v. It is just covered here for your reference in case an older version of Linux or route command is used.

**-V**

The -V option displays route's version, as well as the net-tools version and the protocols supported:

```
[root@lefty /root]# route -V
net-tools 1.54
route 1.96 (1999-01-01)
+NEW_ADDR +RTF_IRTT +RTF_REJECT +I18N
AF: (inet) +UNIX +INET +INET6 +AX25 +NETROM +ATALK +ECONET +ROSE
HW: +ETHER +ARC +SLIP +PPP +TUNNEL +TR +AX25 +NETROM +FR +ROSE +ASH +SIT
+FDDI +HIPPI +HDLC/LAPB
```

## Using *route* to Add Routing Entries

The real power of the route command is to add static routes that affect routing on the local node and, if a routing daemon is running on that local node, affect traffic within the autonomous system as well.

### Adding Routes to Networks

The route command used to add routes takes the following format:

```
route add -net destination netmask gw gateway address
```

For example, to route all traffic destined for 10.1.1.0/24 to the router at 192.168.1.253, use

```
[root@lefty /root]# route add -net 10.1.1.0 netmask 255.255.255.0 gw 192.168.1.253
```

To add a routing entry for a specific host, the -host parameter is used, and the routing entry does not need the netmask parameter. To add a route for 192.168.1.200 to 192.168.1.1, the route command would look like this:

```
[root@lefty /root]# route add -host 192.168.1.200 gw 192.168.1.1
```

This route command would then create an entry that would appear as the following when the route command is entered without any parameters:

```
[root@lefty /root]# route
Kernel IP routing table
```

| Destination | Gateway | Genmask | Flags | Metric | Ref | Use | Iface |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 192.168.1.200 | 192.168.1.1 | 255.255.255.255 | UGH | 0 | 0 | 0 | eth0 |

For PPP networks it is sometimes necessary or preferable to route to a network interface rather than a gateway address. This is used to allow IP addresses to be saved by not using an IP transit network for the serial connection or to create a route when a nonbroadcast network is used. An example follows, but the subject is covered more thoroughly in Chapter 7, "Kernel Support Tools."

```
[root@lefty /root]# route add -net 10.10.10.0 netmask 255.255.255.0 ppp0
```

## ping

ping is a network troubleshooting tool that reports whether or not a remote node is reachable. ping sends an ICMP echo request to the remote node that should then reply with an ICMP echo reply. Because ping and ICMP can be used very effectively to map out a network, many network packet filters and firewalls are configured to drop ICMP to provide tighter security.

Besides checking if a node is responding (or other simple connectivity issues), ping also can be used to troubleshoot other network-related matters. This section covers some of the more advanced parameters of ping that are not well documented. These parameters are based on the ping command that comes with the iputils collection by Alexey Kuznetsov available at ftp://ftp.sunet.se/pub/Linux/ip-routing/. iputils is supplied with most versions of Linux.

### -d

To see additional debugging information provided by the ping command, use the -d parameter. It tells ping to report additional messages that would not be seen, such as an ICMP network unreachable message. The additional information can oftentimes give further insight into the network condition that is causing the ping to fail.

### -f Flood

The -f parameter should be used with caution because it causes Linux to send as many ICMP echo requests as possible, which can quickly cause network problems on burdened networks. The parameter can be used to create a load that simulates a heavy network or to create an additional load on the target machine.

### -i Interval

ping's normal operation is to wait one second before sending the next ICMP echo request. By using the -i interval (in seconds), ping can be told to wait a longer amount of time before sending the next echo request. This can be very useful in network scripts in which it is important to test the network connectivity yet the script needs to be as friendly as possible to the network.
