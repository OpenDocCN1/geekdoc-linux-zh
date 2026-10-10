# Chapter Eight

contain at least three fields: the first is a destination address, the second is the name of the interface to which the datagram is to be routed, and the third is optionally the IP address of another machine which will carry the datagram on its next step through the network. In Linux you can see this table by using the following command:

```
user% cat /proc/net/route
```

or by using either of the following commands:

```
user% /sbin/route -n
user% netstat -r
```

The routing process is fairly simple: an incoming datagram is received, the destination address (who it is for) is examined and compared with each entry in the table. The entry that best matches that address is selected and the datagram is forwarded to the specified interface. If the gateway field is filled, then the datagram is forwarded to that host via the specified interface; otherwise the destination address is assumed to be on the network supported by the interface.

To manipulate this table a special command is used. This command takes command line arguments and converts them into kernel system calls that request the kernel to add, delete, or modify entries in the routing table. The command is called *“route.”*

A simple example. Imagine you have an Ethernet network. You’ve been told it is a class-C network with an address of 192.168.1.0. You’ve been supplied with an IP address of 192.168.1.10 for your use and have been told that 192.168.1.1 is a router connected to the Internet.

The first step is to configure the interface as described earlier. You would use a command like

```
root# ifconfig eth0 192.168.1.10 netmask 255.255.255.0 up
```

You now need to add an entry into the routing table to tell the kernel that datagrams for all hosts with addresses that match 192.168.1.* should be sent to the Ethernet device. You would use a command similar to:

```
root# route add -net 192.168.1.0 netmask 255.255.255.0 eth0
```

Note the use of the “-net” argument to tell the route program that this entry is a network route. Your other choice here is a “host” route, which is a route that is specific to one IP address.

This route will enable you to establish IP connections with all of the hosts on your Ethernet segment. But what about all of the IP hosts that aren’t on your Ethernet segment?