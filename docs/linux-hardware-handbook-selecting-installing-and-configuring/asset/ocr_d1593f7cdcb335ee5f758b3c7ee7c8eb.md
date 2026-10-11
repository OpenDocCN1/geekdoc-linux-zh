# ## Setting the Route

In order to send network traffic, your computer must know to what interface data should be sent. If you only have one Ethernet card, it might seem obvious what interface to use, but it's not quite that simple. Every Linux computer supports a network interface known as the *loopback* device, which refers to the host computer itself. This interface is locked to the 127.0.0.1 IP address, and is configured automatically. You might also use PPP dial-up networking or have a second NIC. For these reasons, you must set up a *routing table*, or *route*, which is a set of rules for the transmission of network traffic.

# ## Routing for a Local Network

Suppose that you're setting up a local network on one interface (let's call it *eth0*). You want traffic destined for computers on this interface to go through *eth0*, but you want other traffic to go through another interface, such as a PPP dialup link or another Ethernet board. In order to configure *eth0*, you use the *route* command, which has the following basic syntax:

```
```
route add | del target [ gw gateway]
```
```

To add a route, you use the *add* parameter and specify the target address or addresses. For instance

```
```
route add 192.168.33.0
```
```

In this example, I've specified an address that ends in *.0*, which is an indication that this is a network address, not just an address for a single computer. In this case, the system sends all data for the 192.168.33.x network through this route. Because you're already bound *eth0* to 192.168.33.2 (using the *ifconfig* command), Linux can determine that this route is associated with the *eth0* device.

# ## Setting the Default Route

Most networked computers have at least two routes: one for the loopback device, and one for everything else. The “everything else” entry sends data through a *router*, or *gateway* computer. The router knows how to send data on to computers on the Internet at large. Thus, your computer doesn't need to know how to access, say, 63.69.110.75; it simply sends all requests for this—or any other address for which it doesn't have a more explicit route—to the gateway system. You set the default route using the *gw* option to the *route* command. For instance

```
```
route add 0.0.0.0 gw 192.168.33.100
```
```

The 0.0.0.0 IP address is shorthand for any address. You can use *default* in place of this number, if you like. The 192.168.33.100 address in this example is the IP address of your network's router. You can obtain this address from your network's administrator.

17
NETWORK HARDWARE