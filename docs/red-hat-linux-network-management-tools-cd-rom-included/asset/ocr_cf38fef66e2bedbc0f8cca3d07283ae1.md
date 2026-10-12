bytes specified with the `-s` option from the 108 bytes transmitted by **ping**. Notice that the response times didn't change much, despite the fact that we used a large data size. We would need to increase the size significantly to observe a larger delay in processing the packets.

You may have noticed that the hostname *d idymus* was used on the command line, but when **ping** echoed back the hostname, it showed a different name, like `d idymus-gw2.home.com`. The reason for this is that *d idymus* is an alias of `d idymus-gw2.home.com`, and using the alias with many UNIX commands results in the official name being returned instead. The alias was created in the `/etc/hosts` file.

The **ping** tool uses a sequence number to keep track of requests and replies. Each request is given the next number in sequence and is then matched with the corresponding reply. This sequencing is used to determine packet loss if any requests do not receive an appropriate reply. Generally speaking, packet loss on a small network should be very rare and, if it does occur, it might indicate a network- or system-related problem. However, on a large network or internet (internet with a lower case *i*) or on the Internet, packet loss is common and represents a normal state of affairs. Given a popular Internet site as shown below, a certain amount of packet loss may be observed:

```
```
ping -c 10 www.whitehouse.gov
PING www.whitehouse.com (209.67.27.247): 56 data bytes
64 bytes from 209.67.27.247: icmp_seq=7 ttl=244 time=240.1 ms
64 bytes from 209.67.27.247: icmp_seq=8 ttl=244 time=240.1 ms
64 bytes from 209.67.27.247: icmp_seq=9 ttl=244 time=240.1 ms

--- www.whitehouse.com ping statistics ---
10 packets transmitted, 3 packets received, 70% packet loss
round-trip min/avg/max = 240.1/240.1/240.1 ms
```
```

The report above indicates that 70% of the packets sent to the `www.whitehouse.gov` system did not have corresponding replies! They were lost. In other words, we sent ten packets, but only received three back; seven out of ten is 70%. One possible reason