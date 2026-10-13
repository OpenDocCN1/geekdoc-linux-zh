restarting `inetd` will fix the problem. If that does not work, rebooting the affected system may be your only option.

# USING `traceroute`

The `traceroute` utility traces the route of UDP packets from the local host to a remote destination. It prints the hostname (if it can be resolved) and the IP address of all routers between the local host and the remote host. If ping cannot reach a particular remote host, it is not always true that the remote host is down. The problem may exist at a gateway somewhere between your system and the remote host. The `traceroute` program can be used to locate such a problem.

`traceroute` uses two special techniques to force an error message to be sent back from each router in its path. It uses a small TTL value (time to live) and an invalid port number. When the packet reaches a router it sends back a “time exceeded” error message. `traceroute` uses this error message to identify the fact that a package has reached a particular router and to calculate roundtrip times. This enables `traceroute` to determine the time required for the hop to the first router. By increasing the time limit value, and re-sending the packet so that it will reach the second router in the path to the destination, which returns another “time exceeded” message, information can be calculated about the second router and so forth. Ultimately, `traceroute` determines when the packet has reached the destination if the destination can be reached. In this way `traceroute` constructs a list of the routers that are traversed to get to the destination host.

Consider the following sample output from a local host (`cstlx001`) to a remote host (`www.bahai.org`):

```
```text
# traceroute www.bahai.org
traceroute to www.bahai.org (207.217.239.32), 30 hops max, 40 byte packets
cstr001 (10.2.0.254) 1.840 ms 1.720 ms 1.657 ms
cstr001-g2 (10.0.2.1) 1.702 ms 1.623 ms 1.606 ms
fw-nat (10.0.0.1) 0.987 ms * *
rtgate (192.115.144.18) 3.631 ms 3.102 ms 3.357 ms
tlv-1f10.netvision.net.il (19.17.193.204) 177.789 ms 16.479 ms 15.654 ms
nyc-s1-0-5-n011.netvision.net.il (194.90.0.54) 360.101 ms 360.117 ms 452.812 ms
nj-ny6t-H5-0-1.netvision.net.il (194.90.0.89) 367.297 ms 384.195 ms 466.206 ms
serial0-1-1.gw2.har1.alter.net (157.130.25.245) 371.438 ms 382.126 ms 372.043 ms
422.ATM9-0-0.GW1.HAR1.ALTER.NET (137.39.30.249) 365.694 ms 366.808 ms 377.897 ms
136.Hssi9-0-0.RNYC2.ALTER.NET (137.39.69.49) 428.716 ms 384.896 ms 387.397 ms
142.ATM3-0.XR1.NYC1.ALTER.NET (146.188.177.34) 391.450 ms 398.219 ms 395.866 ms
195.ATM3-0.TR1.NYC1.ALTER.NET (146.188.178.182) 391.084 ms 382.795 ms 421.005 ms
104.ATM7-0.TR1.LAX2.ALTER.NET (146.188.137.129) 525.664 ms 448.192 ms 516.039 ms
299.ATM6-0.XR1.LAX4.ALTER.NET (146.188.248.249) 447.762 ms 451.041 ms 473.453 ms
193.ATM6-0.GW4.LAX4.ALTER.NET (152.63.113.89) 478.369 ms 486.643 ms 462.203 ms
earthlink-gw.customer.alter.net (157.130.231.222) 477.392 ms 534.410 ms 453.205 ms
18  f9-0-0-cr01-pas.neteng.itd.earthlink.net (207.217.1.107) 537.557 ms 458.573 ms 449.132 ms
19  * f10-1-0-fr01-pas.neteng.itd.earthlink.net (207.217.2.106) 449.583 ms 518.765 ms
20  207.217.208.166 (207.217.208.166) 574.278 ms 514.836 ms 496.682 ms
21  207.217.239.32 (207.217.239.32) 516.840 ms 519.242 ms 526.422 ms
```
```