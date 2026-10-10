single gateway system, though, as described earlier. A simplified version of the *route* syntax is as follows:

```
route [add | del] [-net | -host] target [netmask nm] [gw gw] [reject] [[dev] interface]
```

You specify *add* or *del* along with a *target* (a computer or network address) and optionally other parameters. The *-net* and *-host* options force *route* to interpret the target as a network or computer address, respectively. The *netmask* option lets you set a netmask as you desire, and *gw* lets you specify a router through which packets to the specified *target* should go. (Some versions of *route* use *gateway* rather than *gw*.) The *reject* keyword installs a blocking route, which refuses all traffic destined for the specified network. (This is *not* a firewall, though.) Finally, although *route* can usually figure out the interface device (for instance, *eth0*) on its own, you can force the issue with the *dev* option.

As an example, consider a network in which packets destined for the 172.20.0.0/16 subnet should be passed through the 172.21.1.1 router, which isn't the default gateway system. You can set up this route with the following command:

```
# route add -net 172.20.0.0 netmask 255.255.0.0 gw 172.21.1.1
```

![](bbox=[0.15, 0.455, 0.21, 0.5])

Incorrect routing tables can cause serious problems because some or all computers won't respond. You can examine your routing table by typing *route* alone and compare the results to what your routing table should be. (Consult a network administrator if you're not sure what your routing table should contain.) You can then delete *incorrect* routes and add new ones to replace them, if necessary. Ultimately, of course, changing your configuration files is the best solution, but typing a couple of *route* commands will do the trick in the short term.

One more thing you may need to do if you're setting up a router is enabling routing. Ordinarily, a Linux system won't forward packets it receives from one system that are directed at another system. If Linux is to act as a router, though, it must accept these packets and send them on to the destination network (or at least to an appropriate gateway). To enable this feature, you must modify a key file in the */proc* filesystem:

```
# echo "1" > /proc/sys/net/ipv4/ip_forward
```

This command enables IP forwarding. Permanently setting this option requires modifying a configuration file. Some distributions set it in */etc/sysctl.conf*:

```
net.ipv4.ip_forward = 1
```

Other distributions use other configuration files and options, such as */etc/sysconfig/ sysctl* and its *IP_FORWARD* line. If you can't find it, try using *grep* to search for *ip_forward* or *IP_FORWARD*, or modify a local startup script to add the command to perform the change.