
Most routers send their ICMP messages from the interface “closest” to the destination. If you run **traceroute** backward from the destination host, you may see different IP addresses being used to identify the same set of routers. You might also discover that packets flowing in the reverse direction take a completely different path, a configuration known as asymmetric routing.

Since **traceroute** sends three packets for each value of the TTL field, you may sometimes observe an interesting artifact. If an intervening gateway multiplexes traffic across several routes, the packets might be returned by different hosts; in this case, **traceroute** simply prints them all.

Let’s look at a more interesting example from a host in Switzerland to caida.org at the San Diego Supercomputer Center:³

```
linux$ traceroute caida.org
traceroute to caida.org (192.172.226.78), 30 hops max, 46 byte packets
 1  gw-oekinet.irit7.net (213.144.138.193)  1.122 ms  0.182 ms  0.170 ms
 2  rizur1.core.irit7.net (77.109.128.209)  0.527 ms  0.204 ms  0.202 ms
 3  r1fra1.core.irit7.net (77.109.128.250)  18.279 ms  6.992 ms  16.597 ms
 4  r1ams1.core.irit7.net (77.109.128.154)  19.549 ms  21.855 ms  13.514 ms
 5  r1lon1.core.irit7.net (77.109.128.150)  19.165 ms  21.157 ms  24.866 ms
 6  r1lax1.zenit7.net (82.197.168.69)  158.232 ms  158.224 ms  158.271 ms
 7  ceniC.laap.net (198.32.146.32)  158.349 ms  158.309 ms  158.248 ms
 8  dc-lax-core2--lax-peer1-ge.cenic.net (137.164.46.119)  158.60 ms * 158.71 ms
 9  dc-tus-agg1--lax-core2-10ge.cenic.net (137.164.46.7)  159 ms  159 ms  159 ms
10  dc-sdsc-sdsc2--tus-dc-ge.cenic.net (137.164.24.174)  161 ms  161 ms  161 ms
11  pinot.sdsc.edu (198.17.46.56)  161.559 ms  161.381 ms  161.439 ms
12  rommie.caida.org (192.172.226.78)  161.442 ms  161.445 ms  161.532 ms
```

This output shows that packets travel inside Init Seven’s network for a long time. Sometimes we can guess the location of the gateways from their names. Init Seven’s core stretches all the way from Zurich (zur) to Frankfurt (fra), Amsterdam (ams), London (lon), and finally, Los Angeles (lax). Here, the traffic transfers to ceniC.net, which delivers the packets to the caida.org host within the network of the San Diego Supercomputer Center (sdsc) in La Jolla, CA.

At hop 8, we see a star in place of one of the round trip times. This notation means that no response (error packet) was received in response to the probe. In this case, the cause is probably congestion, but that is not the only possibility. **traceroute** relies on low-priority ICMP packets, which many routers are smart enough to drop in preference to “real” traffic. A few star shouldn’t send you into a panic.

If you see stars in all the time fields for a given gateway, no “time exceeded” messages are arriving from that machine. Perhaps the gateway is simply down. Sometimes, a gateway or firewall is configured to silently discard packets with expired TTLs. In this case, you can still see through the silent host to the gateways beyond. Another possibility is that the gateway’s error packets are slow to return and that **traceroute** has stopped waiting for them by the time they arrive.

3. We removed a few fractions of milliseconds from the longer lines to keep them from folding.

Some firewalls block ICMP "time exceeded" messages entirely. If such a firewall lies along the path, you won't get information about any of the gateways beyond it. However, you can still determine the total number of hops to the destination because the probe packets eventually get all the way there.

Also, some firewalls may block the outbound UDP datagrams that traceroute sends to trigger the ICMP responses. This problem causes traceroute to report no useful information at all. If you find that your own firewall is preventing you from running traceroute, make sure the firewall has been configured to pass UDP ports 33434–33534 as well as ICMP ECHO (type 8) packets.

A slow link does not necessarily indicate a malfunction. Some physical networks have a naturally high latency; UMTS/EDGE/GPRS wireless networks are a good example. Sluggishness can also be a sign of high load on the receiving network. Inconsistent round trip times would support such a hypothesis.

Sometimes, you may see the notation !N instead of a star or round trip time. It indicates that the current gateway sent back a "network unreachable" error, meaning that it doesn't know how to route your packet. Other possibilities include !H for "host unreachable" and !P for "protocol unreachable." A gateway that returns any of these error messages is usually the last hop you can get to. That host usually has a routing problem (possibly caused by a broken network link): either its static routes are wrong, or dynamic protocols have failed to propagate a usable route to the destination.

If traceroute doesn't seem to be working for you or is working slowly, it may be timing out while trying to resolve the hostnames of gateways through DNS. If DNS is broken on the host you are tracing from, use traceroute -n to request numeric output. This option disables hostname lookups; it may be the only way to get traceroute to function on a crippled network.

traceroute needs root privileges to operate. To be available to normal users, it must be installed setuid root. Several Linux distributions include the traceroute command but leave off the setuid bit. Depending on your environment and needs, you can either turn the setuid bit back on or give interested users access to the command through sudo.

Recent years have seen the introduction of several new traceroute-like utilities that can bypass ICMP-blocking firewalls. See the PERTKB Wiki for an overview of these tools at tinyurl.com/y99q6h6u. We especially like mtr, which has a top-like interface and shows a sort of live traceroute. Very neat!

When debugging routing issues, it can be helpful to take a look at your site from the perspective of the outside world. Several web-based route tracing services let you do this sort of inverse traceroute right from a browser window. Thomas Kernen maintains a list of these services at traceroute.org.
