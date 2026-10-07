# Configuring the Routing Table

It's important that a computer knows to which network interface it should send data. When there is just one NIC, this may seem a trivial task, but it's not quite so trivial in Linux, because all Linux systems support a loopback (or localhost) interface which directs the network traffic back to the Linux system. This interface is very useful in troubleshooting and for some basic Linux features, such as X. It's normally assigned an address of 127.0.0.1 and is configured automatically by default startup scripts. You therefore need not concern yourself about the loopback interface, but you must tell your system how to route all other network data.

This task is accomplished with the route command, which has the following syntax:

```
route [add | del] [target] gw gateway
```

Each parameter has a specific meaning:

| add | del | Specify add if you want to add an entry to the routing table, or del if you want to remove one. When starting up an interface, use the add parameter. |
| target | The target is the IP address or network address to which the route applies. A network address looks just like an IP address, but it uses trailing 0% in the mask portion of the IP address, as in 192.168.203.0. One special target is the default route, which is 0.0.0.0. You can use the keyword default in place of 0.0.0.0. If the default route is the route taken by all traffic that's not matched by specific rules. You normally specify a gateway system with the default route; traffic to most sites that aren't on your local network travels through the gateway system. |
 gw gateway | A gateway is a system that knows how to send packets to another network. The terms gateway and router carry very similar meanings, and are often used interchangeably. Your ISP or network administrator can provide you with the IP address of an appropriate gateway.|

> NOTE There's normally no need to specify explicitly the NIC or the IP address with which a route is associated, because the route command can discern this information based on the target or gateway address. If your network is unusually complex, you can force the route to be associated with a device by using the dev parameter.