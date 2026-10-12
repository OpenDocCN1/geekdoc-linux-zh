> **Tip**
> 
> If you issue a route command and it hangs, press Ctrl+C to interrupt it and issue route -n. Issuing route without the -n parameter causes it to do a reverse lookup of every IP in the routing table. If DNS is configured and the host is currently not connected to the network, issuing route by itself can take a long time.

# Manipulating the Routing Table

The route command also adds and removes routes from the routing table. This is done via the following commands:

```
route add|del -net|-host target gw gateway \netmask netmask dev interface
```

The add or del commands indicate, respectively, whether you want to add or delete a route.

The optional -net or -host options indicate whether you want to operate on a net or a host route. (See the following “Host-Based Static Routes” section for more information on net or host routes.) Providing any ambiguity is usually best. For example, the address 10.0.1.0 can be either the network address of a class C network, or the address of a host in a class A or B network.

The target parameter is the host address or network number of the destination. You would use the keyword default as the target for setting or deleting the default route.

The optional gateway parameter indicates which gateway to use for this route. If omitted, the route command assumes that the host or network is connected directly to this host. It’s important to add a route to the local network after configuring an interface with ifconfig:

```
# /sbin/ifconfig eth0 10.1.1.1 netmask 255.255.255.0 broadcast 10.0.1.255
# /sbin/route add -net 10.1.1.0
```

As its name implies, the optional netmask parameter sets the netmask for the route, which will be applied to the target address. If omitted, the netmask will be taken either from the default netmask for the IP address or (in the case of routes to local networks) from the interface’s netmask. (See “Netmasks and Network Classes” earlier in this chapter for more information on the default netmask.)

The optional dev parameter sets the interface on which the packets to this destination will be sent. If omitted, the route command checks the current routing table to find which interface has a route to the gateway. If no gateway is provided, it determines which interface can be used to get directly to the target.