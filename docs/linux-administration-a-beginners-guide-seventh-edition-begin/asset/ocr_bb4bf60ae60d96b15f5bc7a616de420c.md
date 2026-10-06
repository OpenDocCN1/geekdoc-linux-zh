# Linux Administration: A Beginner's Guide

| Destination | Gateway | Genmask | Flags | Metric | Use | Iface |
| 192.168.2.0 | 0.0.0.0 | 255.255.255.0 | U | 0 | 0 | eth1 |
| 192.168.1.0 | 0.0.0.0 | 255.255.255.0 | U | 0 | 0 | eth0 |
| 127.0.0.0 | 0.0.0.0 | 255.0.0.0 | U | 0 | 0 | lo |
| 0.0.0.0 | 192.168.1.8 | 0.0.0.0 | UG | 0 | 0 | eth0 |

A quick check with **ping** verifies that we have connectivity through each route:

```
[root@server ~]# ping -c 1 4.2.2.1
P4.2.2.1 (4.2.2.1) from 192.168.1.15 : 56(84) bytes of data.
64 bytes from 4.2.2.1: icmp_seq=1 ttl=245 time=15.2 ms
<--TRUNCATED...>
1 packets transmitted, 1 received, 0% loss, time 0ms
trt min/avg/max/mdev = 15.277/15.277/15.277/0.000 ms
```

```
[root@server ~]# ping -c 1 192.168.1.30
P192.168.1.30 (192.168.1.30) from 192.168.1.15 : 56(84) bytes of data.
64 bytes from 192.168.1.30: icmp_seq=1 ttl=64 time=0.233 ms
<--TRUNCATED...>
```

```
[root@server ~]# ping -c 1 192.168.2.2
P192.168.2.2 (192.168.2.2) from 192.168.1.15 : 56(84) bytes of data.
64 bytes from 192.168.2.2: icmp_seq=1 ttl=64 time=0.192 ms
<--TRUNCATED...>
```

Looks good. Now it's to enable IP forwarding. This tells the Linux kernel that it is allowed to forward packets that are not destined to it, if it has to route to the destination. This can be done temporarily by setting `/proc/sys/net/ipv4/ip_forward` to 1 as:

```
[root@server ~]# echo "1" > /proc/sys/net/ipv4/ip_forward
```

Hosts on 192.168.1.0/24 network should set their default route to 192.168.1.15, and hosts on 192.168.2.0/24 should set their default route to 192.168.2.1. Most importantly, don't forget to make the route additions and the enabling of **ip_forward** part of the startup scripts.

> TIP Need a DNS server off the top of your head? For a quick query against an external reliable DNS server, try 4.2.2.1, 4.2.2.2, 4.2.2.3, 4.2.2.4, 4.2.2.5, 8.8.8.8, or 8.8.4.4. These addresses have been around for a long time and are composed of a sequence of numbers that is easy to remember. However, be nice about it—a quick query to test connectivity is fine.