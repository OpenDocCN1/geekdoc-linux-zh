An ideal situation is one where an entire IP datagram fits into a frame; and the network it is traveling across supports that particular transfer size. But as we all know ideal situations are rare. One problem with our traveling datagram is that networks enforce a maximum transfer unit (MTU) size, or limit, on the size of transfer. To further confuse the issue, different types of networks enforce their own MTU; for example, Ethernet has an MTU of 1500, FDDI uses 4470 MTU, and so on. When datagrams traveling in frames cross network types with different specified size limits, routers must sometimes divide the datagram to accommodate a smaller MTU. This process is called *fragmentation*.

![](bbox=[0.12, 0.23, 0.21, 0.27])

**Routers provide the fragmentation process of datagrams, and as such, become vulnerable to passive and intrusive attacks.**

# ## IP Addresses, Classes, Subnet Masks

Communicating on the Internet would be almost impossible if a system of unique addressing were not used. To prevent the use of duplicate addresses, routing between nodes is based on addresses assigned from a pool of classes, or range of available addresses, from the InterNetwork Information Center (InterNIC). InterNIC assigns and controls all network addresses used over the Internet by assigning addresses in three classes (A, B, and C), which consist of 32-bit numbers. By default, the useable bits for Classes A, B, and C are 8, 16, and 24 respectively. Addresses from this pool have been assigned and utilized since the 1970s, and they include the ranges shown in Figure 1.6; an example of an IP address is shown in Figure 1.7.

| Class | First Octet or Series | Octets as Network vs. Host | Netmask Binary |
|---|---|---|---|
| A | 1 – 126 | Network.Host.Host.Host | 1111 1111 0000 0000 0000 0000 0000 0000 or **255.0.0.0** |
| B | 128 – 191 | Network.Network.Host.Host | 1111 1111 1111 1111 0000 0000 0000 0000 or **255.255.0.0** |
| C | 192 – 223 | Iletwork.Iletwork.Iletwork.Host | 1111 1111 1111 1111 1111 1111 0000 0000 or **255.255.255.0** |
| D | *Defined for multicast operation and not used for normal operation* |  |  |
| E | *Defined for experimental use and not used for normal operation* |  |  |

**Figure 1.6** IP address chart by class.