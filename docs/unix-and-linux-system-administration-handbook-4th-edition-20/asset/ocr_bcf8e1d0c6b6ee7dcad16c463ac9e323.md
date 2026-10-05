# Chapter 21 Network Management and Debugging

You can use ping to check the status of individual hosts and to test segments of the network. Routing tables, physical networks, and gateways are all involved in processing a ping, so the network must be more or less working for ping to succeed. If ping doesn't work, you are pretty sure that no more sophisticated will work either.

However, this rule does not apply to networks that block ICMP requests with a firewall. Make sure that a firewall isn't interfering with your debugging before you conclude that the target host is ignoring ping. You might consider disabling a medlesome firewall for a short period of time to facilitate debugging.

If your network is in bad shape, chances are that DNS is not working. Simplify the situation by using numeric IP addresses when ping, and use ping'n option to prevent ping from attempting to reverse lookups on IP addresses—lookups also trigger DNS requests.

Be aware of the firewall issue if you're using ping to check your connectivity. Some well-known sites answer ping packets and others. We've found google.com to be a consistent responder.

Most versions of ping run in an infinite loop unless you supply a packet count argument. Under Solaris, ping-s provides the extended output that other versions use by default. Once you have filled of ping, type the interrupt character (usually <Control-C>) to get out.

Here's an example:

```
linux$ ping beast\PING (10.0.1.46): 56 bytes of data.
64 bytes from beast (10.0.1.46): icmp_seq=0 ttl=54 time=48.3ms
64 bytes from beast (10.0.1.46): icmp_seq=1 ttl=54 time=46.4ms
64 bytes from beast (10.0.1.46): icmp_seq=2 ttl=54 time=88.7ms
^\^
-- ping statistics *
3 packets transmitted, 3 received, 0% packet loss, time 2026ms
rtt/avg/max/dev = 46.490/61.202/88.731/19.481 ms
```

The output shows the host's IP address, the ICMP sequence number of each response packet, and the round trip travel time. The most obvious thing that the output above tells you that the server beast is alive and connected to the network.

The ICMP sequence number is a particularly valuable piece of information. Continuities in the sequence indicate dropped packets. They're normally accompanied by a message for each missing packet.

Despite the fact that IP does not guarantee the delivery of packets, a healthy network should drop very few of them. Lost-packet problems are important to be masked by higher-level protocols. The network may appear to function correctly, but it will be slower than it ought to be, not only