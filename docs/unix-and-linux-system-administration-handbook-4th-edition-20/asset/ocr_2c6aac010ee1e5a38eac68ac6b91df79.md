# Linux network hardware options

networking. (This is really just a shorthand to run /etc/rc.d/init/network, which is invoked at boot time with the start argument.)

The startup scripts can also configure static routes. Any routes added to the file /etc/sysconfig/static-routes are entered into the routing table at boot time. The entries specify arguments route add, although in a different order:

```
eth0 net 130.225.248 netmask 255.255.255.248 gw 130.225.204.409
eth1 net 192.38.8.0 netmask 255.255.255.224 gw 192.38.8.129
```

The interface is specified first, but it is actually shuffled to the end of the route command line, which forces the route to be associated with the given interface. (You'll see this architecture in the GUI as where the routes are configured as part of setup for each interface.) The rest of the list consists of route arguments. The static-routes example would also produce the following commands:

```
route -add net 130.225.248 netmask 255.255.255.248 gw 130.225.204.40 eth0
route -add net 192.38.8.0 netmask 255.255.255.224 gw 192.38.8.129 eth1
```

Current Linux kernels do not use the metric parameter to route, but they allow it to be entered into the routing table for using routing daemons.

# Linux network hardware options

The ettool command queries and sets a network interface's media-specific parameters such as link speed and duplex. It replaces the oldii-tool command, but some systems still include both.

You can query the status of an interface just by naming it. For example, eth0 interface (a generic NIC on a PC motherboard) has autonegation enabled and is currently running at full speed:

```
ubuntu~ ettool eth0 [ TP MII ]
Settings for:
Supported ports: 100baseT/Half 100baseT/Full
Supported link modes: 100baseT/Half 100baseT/Full
1000baseT/Half 1000baseT/Full

Supports auto-negotiation: Yes
Advertised link modes: 100baseT/Half 100baseT/Full
1000baseT/Half 1000baseT/Full
1000baseT/Half 1000baseT/Full

Advertised auto-negotiation: Yes
Speed: 1000Mb/s
Duplex: Full
Port: MII
PHYAD: 0
Transceiver: internal
Auto-negotiation: on
Supports Wake-on: pumgb
Wake-on: g
Current message level: 0x00000033 (51)
Link detected: yes
```