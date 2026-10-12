**iface**: Shows which network interface is being used. (eth0 refers to an Internet adapter, and lo refers to the loopback interface. The loopback interface is used internally by the Linux kernel, and you shouldn’t have any need to use it directly.)

The 169.254.0.0 entry is an IPv6 (the next-generation Internet Protocol Version 6) connection. We don’t use IPv6 in this book.

The information about each interface — the routing table — is displayed below the headings. For example, the first line tells Linux to send packets destined for the addresses 192.168.1.0 through 192.168.1.255 to the Ethernet adapter (eth0). The second line deals with the kernel’s internal loopback interface. The third and last line, with the address 0.0.0.0, is the default route. It defines where to send all packets not covered by a specific route.

If your table deviates from the example, you may have a routing problem. For example, if you don’t have the default route, 0.0.0.0, you cannot communicate with any machines on your LAN or the Internet. If you lack a loopback — 127.0.0.1 — route, many internal processes are doomed to fail.

# Defining a route to the loopback interface

You must have a route to the loopback interface (also referred to as lo), which is the 127.0.0.0 address. If you’re missing either or both parameters, you must set them. To set the loopback device, which must be set for the network adapter to work, type this command:

```
route add -net 127.0.0.0
```

To set the route for the network adapter and your local network, type

```
route add 192.168.1.0 dev eth0
```

This route is assigned automatically to your network adapter. You can assign the route to another NIC, if necessary. Here’s an example:

```
route add 192.168.1.0 dev eth1
```

Type netstat -rn to see your routing table. You should see entries for the loopback and Ethernet. If you don’t see a route to your network interface, try repeating the steps. You may have to delete a route. To delete a route, type

```
route del 192.168.1.0 dev eth0
```

Note that you use the network address rather than a host address here. The zero (0) designates the Class-C network address 192.168.1.