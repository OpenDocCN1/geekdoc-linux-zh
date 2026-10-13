For instance, to add the router with the IP address `10.10.10.1` as a default gateway and to tell a host to send packets to the router through the `eth0` interface, use the following command:

```
```text
# /sbin/route add default gw 10.10.10.1 dev eth0
# /sbin/route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
10.10.10.10     *               255.255.255.255 UH    0      0      0   eth0
10.10.10.0      *               255.255.255.0   U     0      0      0   eth0
127.0.0.0       *               255.0.0.0       U     0      0      0   lo
default         10.10.10.1      0.0.0.0         UG    0      0      0   eth0
```
```

Notice that the output of the route command now includes a default destination through a gateway at `10.10.10.1`.

If you want to add a static route to a network, use the command as follows:

```
```text
# /sbin/route add -net <network address>/<network bits>
=> gw <router IP address> dev <ethernet device>
```
```

For instance, to create a static route to the class C network `10.10.20.0` through the router at IP address `10.10.10.2` and to send packets to the router through the `eth0` interface, use the following command:

```
```text
# /sbin/route add -net 10.10.20.0/24 gw 10.10.10.2 dev eth0
# /sbin/route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
10.10.10.10     *               255.255.255.255 UH    0      0      0   eth0
10.10.20.0      10.10.10.2      255.255.255.0   UG    0      0      0   eth0
10.10.10.0      *               255.255.255.0   U     0      0      0   eth0
127.0.0.0       *               255.0.0.0       U     0      0      0   lo
default         10.10.10.1      0.0.0.0         UG    0      0      0   eth0
```
```

> > **Note**
> > 
> > Notice the use of the form `10.10.20.0/24` to specify the network address of the `10.10.20.0` class C network. This syntax is discussed in Chapter 13, “Linux Network Configuration and TCP/IP.”

You can also add a static route to a particular host through a gateway using a similar command. For instance, to define a route to the host `10.10.30.100` through the router with the IP address `10.10.10.3` and using the `eth0` device, use the following command:

```
```text
# /sbin/route add -host 10.10.30.100 gw 10.10.10.3 dev eth0
# /sbin/route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
10.10.10.10     *               255.255.255.255 UH    0      0      0   eth0
10.10.30.100    10.10.10.3      255.255.255.255 UG    0      0      0   eth0
10.10.20.0      10.10.10.2      255.255.255.0   UG    0      0      0   eth0
10.10.10.0      *               255.255.255.0   U     0      0      0   eth0
127.0.0.0       *               255.0.0.0       U     0      0      0   lo
default         10.10.10.1      0.0.0.0         UG    0      0      0   eth0
```
```