# Networking and Internet Services
PART II

| 127.0.0.0 | * | 255.0.0.0 | U 0 0 | 2 |
| w10 | | | | |
| default | router.company. 0.0.0.0 | UG 0 0 | 71 |
| eth0 | | | | |

The output has eight columns:

+   1. The first column (Destination) indicates the route destination. The name is substituted if a corresponding entry exists in either /etc/hosts or /etc/networks. The special name default indicates the default gateway.
2. The second column (Gateway) indicates the gateway through which packets to this destination are sent. An asterisk (*) means that packets will be sent directly to the destination host.
3. The third column (Genmask) indicates the netmask that applies to this route. The netmask is applied to the value in the Destination column.
4. The fourth column (Flags) can have several values. The most common flags are
   U Route is up. This route is enabled.
   H Target is a host. This is a static route to a specific host (see "Host-Based Static Routes" in this chapter).
   Gateway will be used.
   G Use a gateway. That packet will not be sent directly to destination host. The Gateway will be used.
5. The fifth column (Metric) indicates the distance to the target. This is used by some routing daemons to dynamically calculate the best route to a target host.
6. The sixth column (Ref*) isn't used in the Linux kernel. In other UNIX systems it indicates the number of references to this route.
7. The seventh column (use) is the number of times the kernel has performed a lookup for the route.
8. The eighth column (iFace) shows the name of the interface through which packets directed to this route will be sent.

There will be at least one active route—the localhost route, which is set up automatically during system startup. There should also be at least one route per network interface, pointing to the network the interface is connected to.

The -n option modifies the display slight. It doesn't host or network name lookups, displaying instead numerical addresses:

```
$ /bin/route -n
Kernel IP routing table
Destination Gateway Genmask Flags Metric Ref Use
```