![](bbox=[0.24, 0.09, 0.74, 0.32])

**FIGURE 27.9**  A more complex gateway setup. In this case, simba acts as a default router for its own network as well as serving as the default router for falcon, which is itself a default router for another network.

The network served by falcon owns a Class C address block. Notice that all the addresses on the network begin with the base address of 205.211.117.xx. Also, notice that falcon has an IP address of 169.151.116.121. To get simba to route packets to the network served by falcon, we can add the following lines to /etc/rc.conf:

```
defaultrouter="212.214.111.59"
static_routes="*falcon"
falcon="-net 205.211.117.0 169.151.116.121"
```

In this case, the IP address 212.214.111.59 is the default router for simba. In other words, any packets that simba receives that are for hosts it doesn't know about will be sent to this router. 212.214.111.59 is the router at the Internet backbone provider that serves simba.

We have also added what is called a *static route*. This is an entry in the routing table that is static—it does not change. In this case, we have told simba that any packets it receives that have a destination with a base address of 205.211.117.0 should be routed to the address 169.151.116.121. This is the IP address of falcon, which itself serves as a router for another network. As you can see, all the hosts on the network served by falcon begin with an IP address of 205.211.117.xx. Therefore, any packets that simba receives that are intended for any of these hosts will be routed to falcon rather than to the default route of 212.214.111.59. In addition, any packets received by simba that are intended for clients on its own network will be routed directly to those clients rather than sent to the default route.

In order for the static routes to take effect, you will need to reboot the system. It is recommended that you reboot the system, but if you do not want to, you can add the static routes manually so they will take effect immediately. In the previous example, this can be done with the following command from a root shell:

```
route add -net 205.211.117.0 169.151.116.121
```