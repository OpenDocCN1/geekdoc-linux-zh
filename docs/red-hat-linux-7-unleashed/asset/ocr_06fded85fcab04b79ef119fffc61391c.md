+   2. The second column (**Gateway**) indicates the gateway through which packets to this destination are sent. An asterisk (* *) means that packets will be sent directly to the destination host.
+   
+   3. The third column (**Genmask**) indicates the netmask that applies to this route. The netmask is applied to the value in the **Destination** column.
+   
+   4. The fourth column (**Flags**) can have several values. The most common flags are:
+      - `U` Route is up. This route is enabled.
+      - `H` Target is a host. This is a static route to a specific host (see “Host-Based Static Routes” later in this chapter).
+      - `G` Use a gateway. That packet will not be sent directly to the destination host. The gateway will be used instead.
+   
+   5. The fifth column (**Metric**) indicates the distance to the target. This is used by some routing daemons to dynamically calculate the best route to get to a target host.
+   
+   6. The sixth column (**Ref**) isn’t used in the Linux kernel. In other UNIX systems it indicates the number of references to this route.
+   
+   7. The seventh column (**Use**) is the number of times the kernel has performed a lookup for the route.
+   
+   8. The eighth column (**Iface**) shows the name of the interface through which packets directed to this route will be sent.

There will always be at least one active route--the localhost route, which is set up in the `/etc/init.d/network` script. There should also be at least one route per network interface, pointing to the network the interface is connected to.

The `-n` option modifies the display slightly. It doesn’t do host or network name lookups, displaying instead numerical addresses:

```
$ /sbin/route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref  Use Iface
10.0.1.0        0.0.0.0       255.255.255.0   U     0      0    16 eth0
127.0.0.0       0.0.0.0       255.0.0.0       U     0      0    2 lo
0.0.0.0         10.0.1.254    0.0.0.0         UG    0      0    71 eth0
```

In this case, the default destination and the `*` gateway are replaced by the address `0.0.0.0`. This output format is often more useful than the standard output format because there is no ambiguity as to where things are going.