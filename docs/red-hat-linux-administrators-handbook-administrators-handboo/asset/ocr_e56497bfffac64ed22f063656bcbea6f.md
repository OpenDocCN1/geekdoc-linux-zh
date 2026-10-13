properly, the network traffic will be separated between these networks. For example, when a user in the marketing department wants to communicate with another computer in the same department, the network traffic between these two computers will remain in their network. The same is true for the engineering side. Communication between different departments' computers is also allowed. Such internetwork traffic is forwarded to and from these networks by the gateway computer. The end result is a speedier network, because not all users are on the same, large network anymore. A description of how you can implement such a solution follows.

When a full network, such as 192.168.1.0, needs to be divided into subnets, the computer needs a way to determine which IP address belongs to which network. For example, the computer with the network interface 192.168.1.1 is in the marketing department needs to know whether 192.168.1.129 is in the same network so that it can determine whether or not it should send packets destined for 192.168.1.129 to the gateway computer for further forwarding tasks. It can determine whether an IP address belongs to its own subnet by using a network mask, or netmask.

Before you can create a subnet from a network, you need to understand how to create a netmask. For example, suppose you want to determine the network mask for the network 192.168.1.0. This address in binary format looks as follows:

```
11000000.10101000.00000001.00000000
```

Because this is a class C address, the network bits are the first 24 bits (3 bytes). To create the mask, you must set all of these bits to 1's and set the remaining (host interface) bits to 0's. So, the netmask looks as follows:

```
11111111.11111111.11111111.00000000
```

In decimal format, this looks like 255.255.255.0. So, when creating a netmask, you simply need to remember that the network bits are all 1's and the host bits are all 0's. For example, the netmask for the class A network 10.0.0.0 is 255.0.0.0, and, similarly, the netmask for the class B network 129.1.0.0 is 255.255.0.0.

In a TCP/IP network, when a computer wants to send a packet to an IP address, it determines whether or not the IP address is local by performing a bitwise AND operation. For example, to determine whether 192.168.1.1