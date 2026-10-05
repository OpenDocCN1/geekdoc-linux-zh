# 394 CHAPTER 10 NETWORKING AND THE INTERNET

reply. This exchange is a quick way to verify that a remote system is available and to check well the network is operating, such as fast it is or whether it is dropping packets. The ping utility uses the ICMP (Internet Control Message Protocol) protocol. Without any options, ping tests the connection once per execution with CONTROL-C.

```
$ ping www.slashdot.org
PING www.slashdot.org (216.34.181.48) 56(84) bytes of data.
64 bytes from slashdot.org (216.34.181.48): icmp_seq=1 ttl=238 time=70.2ms
64 bytes from slashdot.org (216.34.181.48): icmp_seq=2 ttl=238 time=72.6ms
64 bytes from slashdot.org (216.34.181.48): icmp_seq=3 ttl=238 time=57.5ms
64 bytes from slashdot.org (216.34.181.48): icmp_seq=4 ttl=238 time=71.2ms
--- www.slashdot.org ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 302ms
rtt min/avg/max/mdev = 57.553/68.999/72.605/6.039ms
CONTROL-C
```

This example shows that it is unable to a connection to www.slashdot.org is redirected to slashdot.org and that the system is up and available over the network.

By default ping sends packets containing 64 bytes (55 data bytes and 8 bytes of protocol header information). In the preceding example, four packets were sent to the system slashdot.org before the user interrupted by sending CONTROL-C. The four-part number in parentheses on each line is the remote system's IP address. The packet sequence number (named icmp_seq) is also given. If a packet is dropped, a gap occurs in the sequence numbers. The round-trip time is listed; it represents the time (in milliseconds) that elapsed when the packet was sent from the local system to the remote system and received by the local system. This time is affected by the distance between the two systems, network traffic, and the load on both computers. Before it terminates, ping summarizes the results, indicating how many packets were sent and received as well as the minimum, average, maximum, and mean deviation round-trip times measured. Use ping6 for IPv6 networks.

# When ping cannot connect

if it is unable to contact the remote system, ping continues trying until you interrupt it with CONTROL-C. A system may not answer for any of several reasons: The remote computer may be down, the network interface or some part of the network between the systems may be broken, a software failure may have occurred, or the remote memory may be set, for reasons of security, not to return pings (try ping www.microsoft.com or www.ibm.com).

# traceroute: TRACES OVER THE INTERNET

The traceroute utility (traceroute package) traces the route that an IP packet follows, including all intermediary points traversed (called network hops), to its destination (the argument to traceroute—an Internet host). It displays a numbered list of hostnames, if available, and IP addresses, together with the round-trip time it took for a packet to reach