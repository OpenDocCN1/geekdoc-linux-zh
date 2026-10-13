related task, when a system has two or more network devices, of setting up a special route, using a nondefault device, to a specific network.

# Configure a Default Route

The default route is the path taken by a network message, when the destination address is on an outside network. When a Dynamic Host Configuration Protocol (DHCP) server is working, and is configured to assign gateway addresses, a default route is assigned with the dynamic IP address. That's normally evident in the output to the route -n and netstat -nr commands discussed in Chapter 5. One sample of such output for a system that uses a DHCP server is shown here:

```
Destination Gateway Genmask Flags Metric Ref Use Iface
192.168.122.0 0.0.0.0 255.255.255.0 U 0 0 0 eth0
0.0.0.0 192.168.122.1 0.0.0.0 UG 0 0 0 eth0
```

To review, the default IPv4 address is 0.0.0.0, so the default route goes through the gateway address of 192.168.122.1. In a similar fashion, the default route for a statically configured network system is configured with the GATEWAY directive in its configuration file. Such configuration files are stored in the /etc/sysconfig/network-scripts directory, with names like ifcfg-eth0.

But there are situations, such as a temporary disconnect on a network cable, where the default route is not given by a DHCP server. Perhaps the DHCP server has to be replaced, and you'll have to set up static IP address information. In such cases, the output to the route -n command might look more like the following:

```
Destination Gateway Genmask Flags Metric Ref Use Iface
192.168.122.0 0.0.0.0 255.255.255.0 U 0 0 0 eth0
```

In other words, since the default IP address of 0.0.0.0 is missing, there is no default route. That route can be added temporarily with the route add command. For example, the following command would restore the default route shown earlier:

```
# route add default gw 192.168.122.1
```

If multiple network devices exist on the local system, you can specify it; just for variety, the following command specifies the second Ethernet adapter, eth1:

```
# route add default gw 192.168.122.1 dev eth1
```

To make sure that default route survives a reboot, you'll need to make sure either the system configures that default gateway IP address as part of a static configuration, or the DHCP server used for the network can assign that gateway IP address. To review, Figure 12-5 reflects the way the default gateway IPv4 address is configured