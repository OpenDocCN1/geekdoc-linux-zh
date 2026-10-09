
## Tuning Your Network

After you have your server hardware, operating system, and the Apache server itself tuned for performance, the next typical area of bottleneck is the network itself.

To tune your network you must know the network architecture. Most Web servers are run from an Ethernet network — be it at the office network or at a co-location facility in an ISP. How this network is configured makes a great deal of difference. For example, if you have an Apache server connected to an Ethernet hub, which is, in turn, connected to other hubs that are connected to either workstations or servers, you have a great breeding environment for major bottlenecks. Each machine sees all the traffic on the network; the number of packet collisions increases, and network slow-down is more common. However, such a bottleneck is easily remedied by using network switches in place of hubs.

No special hardware is needed on the devices that connect to an Ethernet switch. The same network interface used for shared media 10Base-T hubs will work with an Ethernet switch. From that device’s perspective, connecting to a switched port is just like being the only computer on the network segment.

One common use for an Ethernet switch is to break a large network into segments. While it is possible to attach a single computer to each port on an Ethernet switch, it is also possible to connect other devices such as a hub. If your network is large enough to require multiple hubs, you could connect each of those hubs to a switch port so that each hub is a separate segment. Remember that if you simply cascade the hubs directly, the combined network is a single logical Ethernet segment.

### Using fast Ethernet

The traditional Ethernet is 10MB/sec, which simply is not enough in a modern business environment that includes e-mail-based communication, Internet access, video conferencing, and other bandwidth-intensive operations. The 100MB/sec Ethernet is the way to go. However, 100 MB/sec or “fast” Ethernet is still quite expensive if you decide to go with fast switches as well. I recommend that you move toward a switched fast Ethernet from now on unless you have already done so. The migration path from 10MB/sec to 100MB/sec can be quite expensive if you have a lot of computers in your network. Each computer in your network must have a 100MB/sec-capable NIC installed, which can be expensive in terms of cost, staff, and time. For a large LAN with several hundred users or more, you should do the upgrade one segment at a time. You can start by buying 10/100MB dual-speed NICs, which will enable you to support your existing 10MB/sec and your upcoming 100MB/sec infrastructure seamlessly.

Using fast Ethernet hand-in-hand with switching hardware can bring a high degree of performance to your LAN. You should definitely consider this option if possible. If you have multiple departments to interconnect, consider an even faster solution between the departments: The emerging Gbit/sec Ethernet standard is very suitable for connecting local area networks together to form a wide area network (WAN).

## Understanding and controlling network traffic flow

Understanding how your network traffic flows is the primary key in determining how you can tune it for better performance. Take a look at the network segment shown in Figure 22-3.

## Knowing your hubs from your switches

The major difference between an Ethernet hub and switch is that each port on a switch is its own logical segment. Computer connected to a port on an Ethernet switch has a full set of bandwidth ascribed to it and need not contend with other computers. A main reason for purchasing a switch over a hub is for its address-handling capabilities. Whereas a hub will not look at the address of data packet and just forward data to all devices on the network, a switch is supposed to read the address of each data packet and correctly forward the data to the intended recipient(s). If the switch does not correctly read the packet address and correctly forward the data, it has no advantage over a hub. The following table lists the major differences between hub and switch.

| Feature | Ethernet Hub | Ethernet Switch |
| :--- | :--- | :--- |
| **Bandwidth** | Total network bandwidth is limited to the speed of the hub, that is, a 10Base-T hub provides a 10MB bandwidth, no matter how many ports exist. | Total network bandwidth is determined by the number of ports on the switch, that is, a 12-port 100MB switch can support up to 1200MB/sec bandwidth – this is referred to as the switch’s maximum aggregate bandwidth. |
| **Duplex Capability** | Supports half-duplex communications limiting the connection to the speed of the port, that is, 10MB port provides a 10MB link. | Switches that support full-duplex communications offer the capability to double the speed of each link from 100MB to 200MB. |
| **Interconnection** | Hop count rules limit the number of hubs that can be interconnected between two computers. | Allows users to greatly expand networks; there are no limits to the number of switches that can be interconnected between two computers. |
| **Cost** | Cheaper than switches. | More expensive than hubs but price/performance is worth the higher price. |

![](img/e11fcbd2818a3495ac70085e5d8d1c26_642_0.png)

Figure 22-3: An inefficient Web network

Here, three Web servers are providing Web services to the Internet and they share a network with an NFS server and a database server. What’s wrong with this picture? Well, several things are wrong. First, these machines are still using dumb hubs instead of a switch. Second, the NFS and database traffic is competing with the incoming and outgoing Web traffic. If a Web application needs database access in response to a Web request, it generates one or more database requests, which, in turn, takes away from the bandwidth available for other incoming or outgoing Web requests, effectively making the network unnecessarily busy or less responsive.

How can you solve such a problem? By using a traffic-control mechanism, of course! First determine what traffic can be isolated in this network. Naturally, the database and NFS traffic is only needed to service the Web servers. In such a case, NFS and database traffic should be isolated so that they do not compete with Web traffic. Figure 22-4 shows a modified network diagram for the same network.

Here, the database and the NFS server are connected to a switch that is connected to the second NIC of each Web server. The other NIC of each Web server is connected to a switch that is, in turn, connected to the load-balancing hardware. Now, when a Web request comes to a Web server, it is serviced by the server without taking away from the bandwidth of other Web servers. The result is a tremendous increase in network efficiency, which trickles down to a more positive user experience.

After you have a good network design, your tuning focus should shift to applications and services that you provide. Depending on your network load, you might have to consider deploying multiple servers of the same kind to implement a more responsive service. This is certainly true for the Web. The next section discusses how you can employ a simple load-balancing scheme by using a DNS trick.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_643_0.png)

Figure 22-4: An improved Web network

## Balancing load using the DNS server

The idea is to share the load among multiple servers of a kind. This typically is used for balancing the Web traffic over multiple Web servers. This trick is called round-robin Domain Name Service.

Suppose that you have two Web servers, www1.yourdomain.com (192.168.1.10) and www2.yourdomain.com (192.168.1.20) and you want to balance the load for www.yourdomain.com on these two servers using the round-robin DNS trick. Add the following lines to your yourdomain.com zone file:

```
www1    IN    A    192.168.1.10
www2    IN    A    192.168.1.20

www     IN    CNAME    www1
www     IN    CNAME    www2
```

Restart your name server and ping the www.yourdomain.com host. You will see the 192.168.1.10 address in the ping output. Stop and restart pinging the same host, and you'll see the second IP address being pinged, because the preceding configuration tells the name server to cycle through the CNAME records for www. In other words, the www.yourdomain.com host is both www1.yourdomain.com and www2.yourdomain.com.

Now, when someone enters www.yourdomain.com, the name server gives out the first address once, then gives out the second address for the next request, and keeps cycling between these addresses.
