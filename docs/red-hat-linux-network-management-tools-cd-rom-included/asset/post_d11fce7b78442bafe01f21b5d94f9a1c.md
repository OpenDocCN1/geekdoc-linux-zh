
For this noticeable packet loss is that some of the critical Internet routers might be quite busy or even overloaded with network traffic. As a result, some of the ICMP requests might be discarded because the requests expired before they were delivered to the final destination. Also, the relative load of the target device can be a factor because these systems might not have the computing resources to answer all network requests as required. Because of the popularity of this site, it is not unreasonable to think that both the servers and the networks that connect them are all quite busy or even overloaded. An overloaded condition will occur when too many users are using resources from the system at the same time.

Sometimes it is desirable to provide additional time for acknowledging each **ping** request instead of using the default value of one second. If additional time is desired between successive ICMP requests, the `-i` option can be used, followed by the desired value. The interval should be long enough to provide the required amount of time for the remote system to respond. When we increase the timeout value as suggested, we will generally notice less packet loss. The command

```
ping -c 10 www.whitehouse.gov -i 5
```

adds a five-second delay to each request, thus providing additional time for the processing of the requests through the network and to the destination server. Using the command above, the following was produced:

```
PING www.whitehouse.com (209.67.27.247): 56 data bytes
64 bytes from 209.67.27.247: icmp_seq=1 ttl=244 time=240.1 ms
64 bytes from 209.67.27.247: icmp_seq=2 ttl=244 time=240.1 ms
64 bytes from 209.67.27.247: icmp_seq=3 ttl=244 time=240.0 ms
64 bytes from 209.67.27.247: icmp_seq=4 ttl=244 time=240.0 ms
64 bytes from 209.67.27.247: icmp_seq=5 ttl=244 time=250.1 ms
64 bytes from 209.67.27.247: icmp_seq=6 ttl=244 time=240.1 ms
64 bytes from 209.67.27.247: icmp_seq=7 ttl=244 time=240.1 ms
64 bytes from 209.67.27.247: icmp_seq=8 ttl=244 time=240.2 ms
64 bytes from 209.67.27.247: icmp_seq=9 ttl=244 time=250.1 ms

--- www.whitehouse.com ping statistics ---
10 packets transmitted, 9 packets received, 10% packet loss
round-trip min/avg/max = 240.0/242.3/250.1 ms
```

As noted from the output, the packet loss to this site was reduced to 10%. Bear in mind that other factors could have also contributed to the reduction, such as users leaving the site or the network not being used. In general, increasing the amount of time for each request should reduce the overall load on the system. However, this is not guaranteed to always be the case because the system may be overloaded to the point that no additional amount of time would really help.

## Miscellaneous Options

With the `-n` option, ping displays IP addresses rather than hostnames. This is useful, for example, when network problems involving DNS impact the use of ping. This option instructs ping not to invoke hostname resolution, thus permitting the tool to function while the name service is slow or temporarily disabled.

The `-R` option enables the record route option with the IP protocol. Toggling the record route informs each router along a path to place its IP address in the IP header. As a result, a list of routers that were used to reach the final destination can be obtained. This is the chief mechanism that the traceroute command utilizes. This tool is described later in this chapter. Another interesting option is flood mode using the `-f` option. This option tells ping to attempt to flood the network with ICMP requests approximately 100 times per second or as fast as the remote destination can process each request.

By the way, a note of caution is in order here; the `-f` option can be a dangerous thing. It can consume a significant amount of network bandwidth and cause systems to suffer from the network because they are too heavily loaded to respond to other network requests. It is not recommended that this option be used on a live network when loss of connectivity could impact the business operations of the individuals that use the network. Also, it is not reasonable to flood other networks that you are not associated with. Having said all this, the command

```
ping -c 100 -f durer
```

displays the following output:

```
PING durer.home.com (10.0.2.10): 56 data bytes
.........
--- durer.home.com ping statistics ---
1015 packets transmitted, 1000 packets received, 1% packet loss
round-trip min/avg/max = 1.0/14.3/121.0 ms
```

The first thing that is different from the standard output is that a series of dots (..........) is shown. This indicates that ping has received responses back from the requests sent to durer. Second, notice that out of 1015 packets sent, only 1000 packets were received. Yet ping reported only a 1% packet loss. Actually, the packet loss is closer to 1.5%. The ping command reports only whole numbers, not numbers to the right of the decimal point. In this case, the problem isn't significant, since we can determine more accurate loss by hand if necessary. However, this is somewhat moot since the ping facility isn't really considered the most scientific and/or empirical approach to measuring data loss or throughput on a network.

Perhaps to many, the important question is, "Why use the flood capability anyway?" The reason is simple: attempt to produce a significant amount of traffic on the network and see what happens. You will find that in networking, determining how things work sometimes includes attempting to break things or do things in such a way as to exceed the practical limitations of a device or system. In the case of networking devices such as routers, industry experts and users want to know what will happen to the device if it is exposed to high-traffic patterns. Measuring performance and other networking characteristics when the network is under tremendous load will help the network manager truly understand the behavior of critical networking devices and systems when they are deployed in their networks. The flood option is one easy way to do this.

The final interesting ping option is quiet mode. This option `-q` is used to limit the amount of output that would normally be produced. The command

```
ping -c 100 dudyamos
```

would produce a large number of lines (over 100) that represented each request and associated reply. With the `-q` option, only a few lines are displayed; the beginning and the summary:

```
ping -c -q 100 didymus
PING didymus-gw2.home.com (10.0.2.127): 56 data bytes
--- didymus-gw2.home.com ping statistics ---
100 packets transmitted, 100 packets received, 0% packet loss
round-trip min/avg/max = 1.1/1.1/2.5 ms
```

Clearly, this option reduces the output, which may be just what is necessary when **ping** is used within a script.

## Tcpdump Tool

### General Description

The **tcpdump** command is a general-purpose network traffic monitor that can capture and display packets and their contents. This command can be used as a *protocol analyzer*, providing one of the best ways to investigate communication and/or connectivity problems among systems and networking devices. Most of the time, network troubleshooting focuses on network configuration problems and diagnosing hardware-related failures. Every now and then, however, you will be faced with a protocol-related problem and forced to delve into the heart of the particular protocol to resolve the problem. With **tcpdump**, the packets scanned will be displayed with information in either a short or long format, depending on the command-line options used. Also, **tcpdump** has a very powerful filtering mechanism that can search for packets that match a specific string or criteria.

Two primary capture modes are provided by **tcpdump**: *promiscuous* and *non-promiscuous*. In promiscuous mode, every packet transmitted on the network is captured, whether or not the packet was sent to the system on which **tcpdump** is executing. This is the mode, for instance, that RMON probes use when monitoring network traffic. Network probes listen on the network for traffic and collect protocol information and statistics. Because Local Area Network (LAN) protocols such as Ethernet are broadcast-based, every frame transmitted can be seen by any network interface attached to the LAN. Any device can read every frame transmitted if that device chooses and is configured to do so. When a device or interface reads every frame from the network, it is said to be in promiscuous mode. In practice, the interface must be configured
