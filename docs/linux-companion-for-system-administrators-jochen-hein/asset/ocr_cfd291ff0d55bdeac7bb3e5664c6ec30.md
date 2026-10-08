# 13.5 All about route

The route program is used for specification of static routes which ensure that other computers in the Internet can be reached. As explained above, direct connection of computers by means of Ethernet is only realistic up to a certain network size. After this, separation into logically connected subnets must be carried out.

Connection between individual subnets is obtained through routers (formerly known as gateways). A router works on the protocol level (for example IP, IPX, or SNA) and can establish a suitable connection on the basis of the information contained in the protocols. In the following sections, we only look at the route of Internet protocols, or IP routing.

The route program is used to establish which computers or networks can be reached via which interface or which IP address is used as default gateway. Provided that the programs routed or gated are activated, routes can be modified by means of different routing protocols. In private local networks this is generally not needed.

A possibility for changing routes dynamically is provided by ICMP redirect messages. A detailed description of this protocol can be found in [rfc0792]. The route command without parameters displays (only under LINUX) the kernel routing tables. The parameter -n causes IP addresses to be output instead of host names, so no name server needs to be interrogated. A better alternative, because it is available on all UNIX systems, this is netstat -r. This command also displays the current routing tables of the kernel in a readable form. This information is provided by the kernel in the file /proc/net/route.

```
(Linux):# route -n
kernel routing table
Destination Gateway Genmask MSS Window Use Iface
192.168.3.0 * 255.255.255.0 U 1872 0 5537 tr0
127.0.0.0 * 255.0.0.0 U 1872 0 41 lo
default 192.168.3.1 * UG 1872 0 0 tr0
```

+   Listing 13.5 Output of the route program.

After activating an interface with ifconfig, computers and networks can be configured by means of route. A route is added with the parameter add. If the route leads to a computer, the corresponding address is prefixed with the keyword -host. If it leads to a network, -net is specified.

![](bbox=[0.226, 0.915, 0.966, 0.998])