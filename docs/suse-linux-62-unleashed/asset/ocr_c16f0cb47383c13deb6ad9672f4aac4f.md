Once you are running a kernel with aliasing enabled, creating an alias is as easy as issuing a standard ifconfig command. All you need to append a colon and an alias number to the interface name. Here is an example:

```
ifconfig eth0:0 10.1.1.1 netmask 255.255.255.0 broadcast 10.1.1.255
```

This creates an alias eth0:0 for Ethernet interface eth0, with the provided parameters.

To automate the creation of an alias each time the host boots, you can add the command to create it to /etc/init.d/network.

# Other ifconfig Options

There are other options to ifconfig for some special circumstances:

ifconfig interface local-address pointpoint remote-address will enable a Point-to-Point interface—one that connects to only a single host, not to a network. The interface must also be enabled in the remote host, switching the local-address and remote-address parameters.

ifconfig local-address tunnel remote-address will create an IPv4 tunnel between two IPv6 networks. IPv4 is the current TCP/IP standard on the Internet. IPv6 is the next-generation IP. If there are any IPv6 networks that need to be connected via the Internet, a tunnel that uses the IPv4 protocol must be made.

# Manipulating the Routing Table: route

The /sbin/route command manipulates the kernel's routing table. This table is used by the kernel to see what needs to be done to leave the host—whether to send it directly to the destination host or to a gateway, and on which network interface to it.

The general form of the route command follows:

```
route [options] [command parameters]
```

# Viewing the Routing Table

The simplest form of the command (with no options and no command) simply outputs the routing table. This form of the command can be utilized by any user:

```
$ /sbin/route
```

```
Kernel IP routing table
```

| IP | Gateway | Netmask | Flags Metric Ref | Use |
| --- | --- | --- | --- | --- | --- | --- |
| iface localnet | | 255.255.255.0 | U | 0 | 0 | 16 |
| eth0 | | | | | |

![](bbox=[0.843, 0.277, 0.952, 0.433])