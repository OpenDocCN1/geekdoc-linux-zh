# UNIX SYSTEM MANAGEMENT PRIMER PLUS

```
bash$ /usr/sbin/traceroute -n 192.168.5.6
troute to 192.168.5.6 (192.168.5.6), 30 hops max, 40 byte packets
1 192.168.1.2 3.711 ms 3.331 ms 2.609 ms
2 192.168.10.5 5.693 ms 5.715 ms 5.670 ms
3 192.168.6.5 5.615 ms 5.534 ms 5.516 ms
4 192.168.5.6 5.975 ms 5.837 ms 5.746 ms
```

There were four hops from the source host to the destination 192.168.5.6. The times reported to the right of each hop are round-trip times for each of three "probes" traceroute sends to the destination.

Devices are not required to answer requests from ping or traceroute. Most firewalls drop these packets, resulting in some skipped hops in the output of traceroute.

```
$ /usr/sbin/traceroute -n 207.8.173.37
traceroute to 207.8.173.37 (207.8.173.37), 30 hops max, 40 byte packets
1 192.168.1.2 3.030 ms 2.796 ms 2.864 ms
2 192.172.25.1 10.044 ms 9.878 ms 9.985 ms
3 208.172.18.62 10.673 ms 10.508 ms 10.487 ms
4 206.24.194.61 13.901 ms 14.281 ms 12.099 ms
5 206.24.195.226 12.928 ms 13.147 ms 11.980 ms
6 144.232.7.105 12.391 ms 12.928 ms 12.361 ms
7 144.232.9.226 63.675 ms 16.622 ms 198.113 ms
8 144.232.14.138 14.910 ms 16.768 ms 14.996 ms
9 144.232.14.42 15.904 ms 15.791 ms 16.542 ms
10 168.81.19.254 15.841 ms 16.488 ms 16.265 ms
11 207.106.31.34 17.621 ms 16.738 ms 16.431 ms
12 207.8.128.93 21.685 ms 20.174 ms 20.364 ms
13 * * *
14 * * *
15 * * *
16 * * *
17 * * *
18 * * *
19 * * *
20 * * *
21 * * *
22 * * *
23 * * *
24 * * *
25 * * *
26 * * *
27 * * *
28 * * *
29 * * *
30 * *
```

# Measuring Packet Loss

One of the scourges of networking is packet loss, or dropped packets. Packet loss occurs when packets fail to reach their destination, causing delays and retransmissions on the client side. Packet loss can result from a variety of problems, including the following: