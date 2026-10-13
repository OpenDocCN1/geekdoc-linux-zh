```
09:21:16.720000 reboot.nitec.com> brat.nitec.com: icmp:
echo request
09:21:16.720000 brat.nitec.com> reboot.nitec.com: icmp:
echo reply
09:21:17.730000 reboot.nitec.com> brat.nitec.com: icmp:
echo request
09:21:17.730000 brat.nitec.com> reboot.nitec.com: icmp:
echo reply
```

Suppose that you are having a problem connecting to an FTP server. You can use tcpdump on your LAN gateway system to see what is going on. For example,

```
tcpdump port ftp or ftp-data
```

displays the FTP-related packets that are originating and arriving to your network.

This allows you to debug a network problem at a low level. If you are experiencing a problem in using a service between two hosts, use tcpdump to identify the problem.

# traceroute

Syntax:

```
traceroute host or IP address
```

This program allows you to locate network routing problems. traceroute displays the routes between two hosts by tricking the gateways between the hosts into responding to an ICMP TIME_EXCEEDED request. Here is an example of a traceroute from my local system to the blackhole.nitec.com host:

```
traceroute to blackhole.nitec.com (209.63.178.15), 30
hops max, 40 byte packets
1 router (206.171.50.49) 4.137 ms 3.995 ms 4.738 ms
2 PM3-001.vl.NET (206.171.48.10) 32.683 ms 33.295 ms
33.255 ms
```