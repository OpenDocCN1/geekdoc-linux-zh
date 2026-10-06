
# UNIX SYSTEM MANAGEMENT PRIMER PLUS

```bash
$ /usr/sbin/traceroute -n 192.168.5.6
traceroute to 192.168.5.6 (192.168.5.6), 30 hops max, 40 byte packets
1 192.168.1.2 3.711 ms 3.331 ms 2.609 ms
2 192.168.10.5 5.693 ms 5.715 ms 5.670 ms
3 192.168.6.5 5.615 ms 5.534 ms 5.516 ms
4 192.168.5.6 5.975 ms 5.837 ms 5.746 ms
```

There were four hops from the source host to the destination 192.168.5.6. The times reported to the right of each hop are round-trip times for each of three "probes" traceroute sends to the destination.

Devices are not required to answer requests from ping or traceroute. Most firewalls drop these packets, resulting in some skipped hops in the output of traceroute.

```bash
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

- Broken cables
- Loose connections
- Failing network interface
- Overloaded network interface
- Malfunctioning switch, firewall, or router
- Bad routing information
- Electromagnetic interference on a cable

You can use ping to detect dropped packets, though for low rates you may need to run it for quite a while before you see evidence of dropped packets. The following output from ping is indicative of a packet loss problem:

```bash
$ ping 192.168.5.1 56 10
PING 192.168.5.1: 56 data bytes
64 bytes from 192.168.5.1: icmp_seq=0, time=6 ms
64 bytes from 192.168.5.1: icmp_seq=1, time=5 ms
64 bytes from 192.168.5.1: icmp_seq=3, time=5 ms
64 bytes from 192.168.5.1: icmp_seq=4, time=5 ms
64 bytes from 192.168.5.1: icmp_seq=5, time=5 ms
64 bytes from 192.168.5.1: icmp_seq=6, time=5 ms
64 bytes from 192.168.5.1: icmp_seq=8, time=6 ms
64 bytes from 192.168.5.1: icmp_seq=9, time=5 ms
---192.168.5.1 PING Statistics
10 packets transmitted, 8 packets received, 20% packet loss
round-trip (ms) min/avg = 5/5
```

In this output, icmp_seq 2 and 7 are missing—either they did not reach 192.168.5.1 or the responses never made it back. The resulting 20% packet loss is significant, but in general, you shouldn't tolerate any packet loss. If you experience dropped packets on one of your WAN interfaces, like a T1 to the Internet, call your provider immediately to diagnose the problem. If the problem is internal to your own network, make sure all of your cables and connections are secure before moving onto routers and switches.

# Measuring Network Errors

When a system detects an error in network communications to or from one of its interfaces, it updates counters in the kernel. You can display these counters with netstat -ni.

```bash
$ netstat -ni
```

| Name | Mtu | Net/Dest Address | Ipkts | Ierrs | Oerrs | Collis Queue |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| lo0 | 8232 | 127.0.0.1 | 246 | 0 | 0 | 0 |
| meme0 | 1500 | 192.168.1.0 | 29138 | 3 | 17460 | 0 | 0 |

UNIX SYSTEM MANAGEMENT PRIMER PLUS

Ierrs are input errors and Oerrs are output errors. Red Hat Linux displays the counters a bit differently, as follows:

```bash
$ netstat -ni
Kernel Interface table
| Interface | Link | encap | HWaddr | Address | Bcast | Mask | MTU | RX packets | Ierrs | TX packets | Oerrs | collisions txuelen |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| eth0 | Ethernet | | 00:10:B5:96:0A:5E | 192.168.1.255 | | 255.255.255.0 | 1500 | 128296 | 3 | 5713105 | 0 | 0 | 100 |
| lo | Loopback | | 127.0.0.1 | | 255.0.0.0 | 3924 | 100713 | 0 | 100713 | 0 | 0 | 0 |

The fast Ethernet interface eth0 (the first example) had three input errors out of 291,389 packets received by an error rate of 0.001 (one error per 100,000 packets). However, you have no way of determining these errors happened. To avoid this problem, you may want to run this command with an interval in seconds as the last argument to view up-to-date statistics every few seconds, like vnstat.

# Don't Accept Errors on Ethernet

Although you can expect a very small error rate on serial interfaces, similar to that of a T1, interfaces on local area networks should very rarely (if ever) experience network errors. If you do see errors on an Ethernet interface, check all cables and connections to make everything is working as it should.

Network errors are caused by a variety of factors, including the following:

- Malformed packets
- Failing interface cards or ports
- Bad cables
- Duplex mismatches

# Buy a Cable Tester

Punctures in the cable shield, loose pin connections, and poorly twisted pairs all take their toll on a signal traveling across that cable. Use a cable tester to verify that a cable is functioning properly; you can purchase one at many retail computer stores and catalogs.

# Chapter 11 • PERFORMANCE TUNING AND CAPACITY PLANNING 325

Physics can also play a role in network errors; interference, crosstalk, and signal degradation are common afflictions on many networks.

Interference occurs when an electromagnetic signal from a device such as a monitor causes a signal to be created in a nearby cable. This signal interferes with the normal signals sent across the cable.

Crosstalk is a type of interference that occurs between two wires transmitting different signals in the same cable. Crosstalk is a problem in cables without twisted-pair wiring.

# Twisted-Pair Wiring

Category 5 and 6 cabling, used for Ethernet networking, twists pairs of wires in each cable. Twisting reduces the strength of any interference caused in each pair, especially crosstalk.

Signal degradation is the gradual weakening of a signal as it travels across the length of a cable. The signal can become so weak that it is not recognized at its destination. The natural resistance of copper wiring and external interference are the major contributors to signal degradation.

# Maximum Cable Lengths

All network transmission protocols (such as 100Mbps Ethernet) specify the maximum length for supported cables; signals cannot be guaranteed to transmit clearly in cables beyond length. For example, 100Mbps Ethernet has a limit of 100 meters over Category 5 cabling. Compare that with Gigabit Ethernet over fiber optic cabling, which has a limit of 2 kilometers!
