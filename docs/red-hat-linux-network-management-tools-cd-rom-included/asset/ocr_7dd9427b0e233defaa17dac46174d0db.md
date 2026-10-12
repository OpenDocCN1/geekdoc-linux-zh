```
```
1 router-1 (10.0.2.129) 4.256 ms * 2.899 ms
2 vermeer (128.197.2.200) 7.340 ms 7.433 ms 7.526 ms
```
```

By default, **traceroute** sends a total of three probes, each with a different TTL value, to every hop. The first line of the output includes the destination along with the IP address, the default number of hops **traceroute** used, and the size of the packets being sent. The second line (with a 1) displays the first hop encountered by **traceroute** (see Figure 4.3).

![](bbox=[0.05, 0.3, 0.95, 0.58])

Figure 4.4 traceroute with two hops.

Because *vermeer* is on a different physical network than *monet*, a router must be used to reach this system. Because the default router in this example is *router-1*, the first packet is sent there. The first packet sent is an ICMP request packet with the TTL field set to 1. With IP, any packet that reaches the router decrements the TTL by 1, which makes it zero. When a router gets a packet and the TTL is zero, it is supposed to discard the packet and notify the sender. This forces the router to respond with a TIME_EXCEEDED message back to *monet*. After this happens, **traceroute** measures the amount of time between when it sent the packet and when it obtained the reply. This is known as the *round-trip time* or RTT and is displayed in milliseconds (1000th of a second) as shown after the hostname and IP address information. This implies that the RTT of the first