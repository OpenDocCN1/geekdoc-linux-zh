be unable to do so. The only IP address ever seen by the outside world is the address of the Red Hat server, and not all the addresses behind it. Even if the miscreant sends a packet to the Red Hat server, the server will have no way of knowing which user machine to forward it to.

By default, the Red Hat Linux kernel has IP masquerading support built in. However, if you have removed some support earlier or are using a kernel that does not have IP masquerading built in, you need to recompile the kernel, load a few modules, and set a packet-filtering rule to allow the address translation to occur. For IP masquerading to work, you need to enable IP forwarding service on the server. You can enable IP forwarding (for the default kernel shipped by Red Hat) by setting FORWARD\_IPV4 to yes in the /etc/sysconfig/network file. This discussion assumes that you are using a kernel with IP masquerading and forwarding support built in, and that you have also installed the ipchains package on the Red Hat server.

To connect your internal network to the outside world, you need two network interfaces on the IP masquerading server. One interface will be used to connect to the internal network, and the other interface will be used to connect the server (and the internal network via IP masquerading) to the outside world. Because such a server has multiple interfaces, it is often called a *multihomed server*. You can assign a private IP address to the network card connected to the internal network. For example:

```
/sbin/ifconfig eth1 inet 192.168.1.1 netmask 255.255.255.0
```

This assumes that your network interface for the internal network is eth1 and that you will be running fewer than 253 user computers within your network. If you are in a situation where you will have more than 253 user computers, you may use a netmask of 255.255.0.0, which allows more than 65,000 user computers behind one Red Hat IP masquerade computer. If you exceed 253 user computers, set up a second IP masquerade computer and divide your network into two subnets.

By configuring your user computers with IP addresses starting at 192.168.1.2 and ending at 192.168.1.254, and by assigning them all a gateway of 192.168.1.1 and a subnet mask of 255.255.255.0, you should be able to ping the gateway (192.168.1.1) from each user computer.

At this point, all the user machines can talk to one another and to the Red Hat server, but a user still can't reach the outside world from a client