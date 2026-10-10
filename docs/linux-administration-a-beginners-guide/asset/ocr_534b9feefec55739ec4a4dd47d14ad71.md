In the case where a host doesn't even have the first clue about where to send a packet, it uses its *default route*. This path points to a router, which ideally does have an idea of where the packet should go or at least knows of another router that can make smarter decisions. A typical Linux host knows of three routes: the first is the loopback route that simply points toward the loopback device. The second is the route to the local area network so that packets destined to hosts within the same LAN are sent directly to them. Finally, the third route is the default route. This route is used for packets that need to leave the local area network to communicate with other networks.

If you set up your network configuration at install time, this setting is most likely already taken care of for you, so you don't need to change it, which, of course, doesn't mean you can't...

> *NOTE*: There are actually instances where you will need to change your routes by hand. Typically, this is necessary when multiple network cards are installed into the same host where each NIC is connected to a different network. You should know how to add a route so that packets can be sent to the appropriate network based on the destination address.

# ## Simple Usage

The typical route command is structured as follows:

```
`[root@ford /root]# route cmd type addy netmask mask gw gw dev dn`
```

The parameters are as follows:

Parameter | Description
cmd | Either add or del depending on whether you are adding or deleting a routing. If you are deleting a route, the only other parameter you need is ifadd.
type | Either -net or -host depending on whether addy represents a network address or a router address.
addy | The destination network that we want to offer a route to.
netmask mask | Sets the netmask of the addy address to mask.
gw gw | Sets the router address for addy to gw. Typically used for the default route.
dev dn | Sends all packets destined to addy through the network device dn as set by ifconfig.

*Example*: Here's how to set the default route on my host, which has a single Ethernet device and a router of `192.168.1.1`:

```
`[root@ford /root]# route add -net default gw 192.168.1.1 dev etho`
```