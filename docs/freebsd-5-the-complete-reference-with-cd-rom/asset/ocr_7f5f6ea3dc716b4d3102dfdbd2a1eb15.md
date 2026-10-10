don't work, you won't see this line; but if hostname resolution works but you can't reach the target system, you'll see that line and no further output.

> **Note**
> If your DNS server isn't on your local network, a DNS failure could in fact be a routing problem. Consult the next section, “Diagnosing Routing Problems,” for further information.

You can also use this method to test resolution of remote hostnames, such as those on the Internet at large. If your DNS server is on your local network segment, it’s possible that this name resolution will work even if you can’t reach the remote site because your local routing configuration might be incorrect.

The host and nslookup commands also test name resolution, and in a more direct way than ping. These commands are designed expressly to return an IP address when given a hostname, or a hostname when given an IP address.

# ### Diagnosing Routing Problems

You can use ping to test basic connectivity between you and a remote system. For instance, you might type the following:

```
$ ping www.osborne.com
PING www.osborne.com (198.45.24.130): 56 data bytes
64 bytes from 198.45.24.130: icmp_seq=0 ttl=238 time=131.518 ms
64 bytes from 198.45.24.130: icmp_seq=1 ttl=238 time=162.523 ms
64 bytes from 198.45.24.130: icmp_seq=2 ttl=238 time=130.061 ms
64 bytes from 198.45.24.130: icmp_seq=3 ttl=238 time=134.463 ms
^C
--- www.osborne.com ping statistics ---
4 packets transmitted, 4 packets received, 0% packet loss
round-trip min/avg/max/stddev = 130.061/139.641/162.523/13.306 ms
```

This test reveals substantially higher latencies than on the local network, but precisely how high depends on your network connection, the distance to the target site, and so on. This example also demonstrates the use of hostname resolution with ping, but it’s possible for your DNS configuration to be bad but your routing to be good. In such a case, you can try entering the IP address of a remote system, if you know it.

If you can reach some external sites but not others, it’s possible that your netmask is set incorrectly, so you should double-check that configuration. Another possibility is that some external router is down or misconfigured, or the problem might reside on the target system. You can help diagnose such problems using traceroute, which generates statistics on the path to every router between you and the target system. For instance, you might type the following command:

```
$ trancerte -n 68.1.0.44
trancerte to 68.1.0.44 (68.1.0.44), 64 hops max, 40 byte packets
```