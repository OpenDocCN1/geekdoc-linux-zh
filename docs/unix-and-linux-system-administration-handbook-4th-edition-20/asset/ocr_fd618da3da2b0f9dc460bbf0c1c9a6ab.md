# Chapter 14

# TCP/IP Networking

# Routing tables

You can examine a machine's routing table with netstat -r. you can also avoid DNS lookups and present all the information numerically, which is generally more useful. We discuss netstat in more detail starting on page 86, here is a short example to give you a better idea of what routes look like:

```
redhat$ netstat -rn
```

| Destination | Genmask | Gateway | Fl | MSS | Iface |
| --- | --- | --- | --- | --- | --- |
| 132.236.270 | 255.255.255.0 | 132.236.227.93 | U | 150 | eth0 |
| default | 0.0.0.0 | 132.236.227.1 | UG | 150 | eth0 |
| 132.236.212 | 255.255.255.192 | 132.236.212.1 | U | 150 | eth1 |
| 132.236.224 | 255.255.255.192 | 132.236.212.6 | UG | 150 | eth1 |
| 127.0.0.1 | 255.255.255 | 127.0.0.1 | U | 358 | lo |

This host has two network interfaces: 132.236.227.93(eth0) on the network 132.236.227/24 and 132.236.212.1 (eth1) on the network 132.236.212.0/26.

The destination is usually a network address, unless add host-specific routes (their genmask is 255.255.255.255 all bits are consulted). An entry's gateway field must contain the full IP address of a local network interface or adjacent host; on Linux kernels it is 0.0.0.0 to invoke the default gateway.

For example, the first route in the table says that to reach the network 132.236.220/64, packets must be sent to the gateway 132.236.212.6 through interface eth1. The second entry is a default route; packets not explicitly addressed to any of the three routes listed (or to the machine itself) are sent to the default gateway, 132.236.227.1.

A host can only reach gateway machines that are reachable through a directly connected network. The local host's job is limited to moving packets one hop closer to their destinations, so it is pointless to include information about nonadjacent routes in the local routing table. Each packet makes a fresh next-hop routing decision based on its own local routing table.¹

Routing tables can be configured statically, dynamically, or with a combination of the two approaches. A static route is one that you enter explicitly with the route command. Static routes remain in the routing table as long as the system is up; they are set up at boot time from one of the system startup scripts. For example, Linux commands

```
# route add -net 132.236.220 netmask 255.255.255.192
gw 132.236.212.6 eth1
# route add default 132.236.227.1 eth0
```

The IP source routing feature is an exception to this rule; see page 473.

See page 481 for information about the route command.

466