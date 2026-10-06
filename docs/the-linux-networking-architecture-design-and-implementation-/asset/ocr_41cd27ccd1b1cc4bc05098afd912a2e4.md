# 576 Appendix C Tools and Commands for Network Operation

# Example

```
root@tux # ping www.Linux-netzwerkarchitektur.de
PING.Linux-netzwerkarchitektur.de (192.67.198.52): 56 data bytes
64 bytes from 192.67.198.52: icmp_seq=0 ttl=224 time=4.589 ms
64 bytes from 192.67.198.52: icmp_seq=1 ttl=224 time=3.481 ms
64 bytes from 192.67.198.52: icmp_seq=2 ttl=224 time=3.271 ms
64 bytes from 192.67.198.52: icmp_seq=3 ttl=224 time=3.785 ms
--- www.Linux-netzwerkarchitektur.de ping statistics ---
4 packets transmitted, 4 packets received, 0% packet loss
round trip min/avg/max = 3.271/3.781/4.589 ms
```

# C3 USING NETSTAT TO VIEW THE NETWORK STATE

netstat is an extensive tool for viewing the network state. For example, you can use netstat to display the routing table and the state of the socket currently created.

Displaying routing tables If you start it with the -r option, netstat outputs the routing tables of the kernel. This corresponds to the result of the route command. The -n is used to output the IP addresses of computers instead of their DNS names.

```
root@tux # netstat -nr
Kernel routing table
```

| Destination Gateway Genmask Flags MSS Window Use Iface |
| 129.13.42.0 0.0.0.0 255.255.255.0 U 0 0 478 eth0 |
| 127.0.0.0 0.0.0.0 255.0.0.0 U 0 0 50 lo |
| 0.0.0.0 129.13.42.233 0.0.0.0 UG 0 0 238 eth0 |

The first column of this output shows the route destination. The Flags show the type of destination (i.e., Gateway (G) or Host (H)), to better explain the entry in the first column.

If there is a gateway (router), the second column shows the IP address of that router (or, more exactly, the IP address of the adapter where the packet arrives in router). If the route does not lead across a gateway, then the second column shows the value 0.0.0.0.

The third column shows the reach of a route. In routes with a (sub)network as the destination, the entry in the third column corresponds to the network mask; the value 255.255.255.255 is output for routes to computers (H). The default route has a mask 0.0.0.0.

All entries in the routing table are sorted so that the most special routes (long network masks) are listed before the more general routes (short network masks). When searching for a matching route, the kernel takes the bit-by-bit AND of the destination and the network mask and compares the result with the route's destination.

The fourth column shows various flags that provide more information about a route. As has been mentioned, these flags specify the type of destination (gateway or host), among other things: