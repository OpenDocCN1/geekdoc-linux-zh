![](bbox=[0.12, 0.11, 0.78, 0.28])

# ## Loopback Route

Let's look at a very simple routing table—the table for a machine with only the a loop-back interface:

```
$ route -n
Kernel IP routing table
Destination Gateway Genmask Flags Metric Ref Use Iface
127.0.0.0 0.0.0.0 255.0.0.0 U 0 0 0 lo
```

Each line in the listing is called a route. Here's what each column means:

+   - **Destination** specifies the destination host or network.
+   - **Gateway** is the IP address of a gateway to use. (*Gateway* is an older term for *router*.) If the gateway address is **0.0.0.0**, it means the destination is directly connected to the host, and no gateway is needed.
+   - **Genmask** is the "generality mask," which specifies the generality of the route. For this route, the genmask is **255.0.0.0**, meaning that only the first eight bits of the destination address need to match the Destination column. Thus, Any packet destined for **127.x.y.z** will use the route. When trying to matching a route for an IP address, the kernel bitwise ANDs the address with the genmask, and then performs the comparison.
+   - **Flags** lists some flags associated with the route. The most common flags are **U** (the route is up), **H** (the target is a host rather than a network), and **G** (use a gateway). Other flags are possible; consult `route(8)` for more details.
+   - **Metric** is a measure of the "cost" of the route.
+   - **Ref** is the count of the number of connections currently using the route.
+   - **Use** is the number of times the route has been used in a routing lookup.
+   - **Iface** is the interface to use.