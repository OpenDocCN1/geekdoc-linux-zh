# ACTIVATING THE NETWORK DEVICES 383

reserved corresponding network. Since it is used in normal operation, this interface must be configured on every TCP/IP computer.

```
# activate loopback interface
/sbin/ifconfig lo 127.0.0.1
# set route
/sbin/route add -net 127.0.0.0
```

Listing 13.1 Initialization of the loopback interface.

Listing 13.2 shows the configuration of an Ethernet card. If the computer is connected to a TokenRing, tr0 must be specified instead of eth0. This not only activates the interface, but it also ensures accessibility of other computers by establishing the corresponding routes. The metrics indicate the 'costs' for these routes, so an economical route can be selected on the Internet.

```
# activate Ethernet interface
/sbin/ifconfig eth0 IPADDR broadcast $ BROADCAST \
netmask $ NETMASK
# set routes
/sbin/route add -net $ NETWORK netmask $ NETMASK
# default route via the gateway $ GATEWAY metric 1
```

Listing 13.2 Initialization of the Ethernet interface.

Listing 13.2 does not indicate the IP addresses, but only shell variables. The real values are either assigned to you locally by your provider or network administrator, or centrally by the Network Information Center. This central assignment of addresses ensures that each address is unique worldwide. In temporary connections to the Internet via SLIP or PPP, these addresses can also be dynamically assigned by the provider at each call. When using PPP, you do not have to worry about anything because the PPP daemons already contain this function.

The broadcast address specifies how all computers in the same subnet be reached, whereas the netmask specifies how to determine whether a computer belongs to the local network or not. A detailed discussion can be found in Section 13.5.1.

All distributions have a configuration tool for networking. How that works and where the configuration is stored varies widely between the distributions. If you are in doubt, check your manual.