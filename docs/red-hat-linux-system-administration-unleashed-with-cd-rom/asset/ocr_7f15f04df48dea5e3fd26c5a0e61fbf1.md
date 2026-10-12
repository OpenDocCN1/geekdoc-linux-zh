# Adding and Deleting Static Routes

The easiest way of adding and deleting static routes under Red Hat 6 is to use Linuxconf. However, it is sometimes necessary to try to repair networks in emergency situations where complex tools are not available. This makes it worth learning to do it by hand, using the route command, and in addition it becomes obvious what happens when you use the configuration tool.

The first argument to route should be one of the words add or del to indicate that the route described by the remaining arguments is being added or deleted, respectively.

The syntax of the remaining arguments depends on the type of route being added. The simplest case is adding the default route. This command looks like

```
route add default gw gateway
```

where gateway is the IP address of the host that will forward packets. Note that for this route to be usable, there must already be a route (usually a static route) for gateway. The gateway can be specified with a hostname, but usually a numeric IP address is used. This is because static routes are usually added at boot time, when there may be no name service running.

For adding non-default routes, the second argument is normally one of the words -net or -host, to indicate whether the route is for a network or a host. However, this argument can be omitted if the route is for a host.

The argument immediately after the -net or -host is the destination IP address (either as a hostname, or as a numeric address). This should be followed by the word netmask and then the actual netmask to be used for this route. The netmask may be omitted if it matches the natural mask for the destination address.

Finally, there must be some indication of the route to take for this destination. If the destination is directly available, use the dev keyword, followed by the device that is to be used (such as eth0). If this is the last part of the command line, the dev keyword can be omitted. If routes for this destination must be forwarded by a gateway, use the gw keyword with the IP address (name or number) of the gateway system. As for the default route, there must be some existing route to the gateway system.

It is also possible to add a rejecting route. Adding the word reject to the end of the route command installs a rejecting route, which forces the route lookup to fail. It is used for masking out networks before using the default route.

Once you can add routes, deleting routes is straightforward. To delete a route, just give the command line that adds the route question, substituting the word del for the word add. Some of the parameters can be removed from the command line, but supplying all the