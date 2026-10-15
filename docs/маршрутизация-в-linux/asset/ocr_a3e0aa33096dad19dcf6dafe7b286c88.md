To capture the output, we will turn off name resolution to avoid further traffic creation and turn on the verbose flag. Below is the output of the traceroute command with the output lines numbered for easy reference.

```
[root@lefty /root]# tcpdump -nv
1 11:56:57.885796 eth0 > 192.168.1.254 > 10.2.2.254: icmp: echo request [ttl 1]
[ id 34072]
2 11:56:57.949353 eth0 < 10.1.1.254 > 192.168.1.254: icmp: time exceeded in-
transit (ttl 64, id 11798)
3 11:56:57.949736 eth0 > 192.168.1.254 > 10.2.2.254: icmp: echo request [ttl 1]
[ id 34073]
4 11:56:57.984039 eth0 < 10.1.1.254 > 192.168.1.254: icmp: time exceeded in-
transit (ttl 64, id 11804)
5 11:56:57.984272 eth0 > 192.168.1.254 > 10.2.2.254: icmp: echo request [ttl 1]
[ id 34074]
6 11:56:58.017169 eth0 < 10.1.1.254 > 192.168.1.254: icmp: time exceeded in-
transit (ttl 64, id 11818)
7 11:56:58.017459 eth0 > 192.168.1.254 > 10.2.2.254: icmp: echo request (ttl 2,
[ id 34075]
8 11:56:58.043489 eth0 < 10.2.2.254 > 192.168.1.254: icmp: echo reply (ttl 254,
[ id 34075]
9 11:56:58.043740 eth0 > 192.168.1.254 > 10.2.2.254: icmp: echo request (ttl 2,
[ id 34076]
10 11:56:58.068649 eth0 < 10.2.2.254 > 192.168.1.254: icmp: echo reply (ttl 254,
[ id 34076]
11 11:56:58.068873 eth0 > 192.168.1.254 > 10.2.2.254: icmp: echo request (ttl 2,
[ id 34077]
12 11:56:58.094390 eth0 < 10.2.2.254 > 192.168.1.254: icmp: echo reply (ttl 254,
[ id 34077]
34 packets received by filter
```

As can be seen in line 1, lefty (192.168.1.254) has sent out three echo requests with the ttl set to 1 to destination 10.2.2.254. The first router 10.1.1.254 decrements the ttl to 0 and then sends back the ICMP: time exceeded message to each of the echo requests as seen in lines 2, 4, and 6. traceroute then increments the ttl 2, which makes it to the destination and the destination then replies (lines 8, 10, and 12).

# Summary

In this chapter, the Linux commands for displaying and configuring Linux nodes have been covered. The common uses of ifconfig, route, ping, traceroute, arp, netstat, and tcpdump have been covered. ifconfig is used to configure and show configuration options for network interface cards. route is used to add and display routing entries on the Linux node.

ping and traceroute are troubleshooting tools used to determine and localize network connectivity issues. And finally, tcpdump is a general-purpose, freely available protocol analyzer available for Linux, definitely recommended for Linux network nodes.