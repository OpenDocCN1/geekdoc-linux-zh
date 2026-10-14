You can also use ping with a host name:

```
$ ping ftp.xmission.com
```

A good practice when testing your network is to begin by pinging your own host name to see that it can be resolved (converted into an IP address). Then ping the host name for another host on your local network, then of a distant host or Internet site. If none of the host name pings works, but the ping command does respond when you use an IP address, then you know that your system is not able to convert domain names into IP addresses because it cannot reach a functioning DNS server.

The basic idea with these ping operations is to ping to hosts further and further away from your system. If something stops working, you know where the error occurred. For example, if you can ping other hosts within your local network segment but not on any other segments, you know that your packet cannot get outside the local segment.

![](bbox=[0.12, 0.55, 0.2, 0.65])

> A warning is in order regarding pinging Internet sites: Because several types of security attacks rely on the ping command, some systems are configured to completely ignore ping packets. This means that when you ping some servers on the Internet, you will see no response even though the network connection works fine!

One example of a ping-based security attack is the "flood ping," which sends many ping commands in rapid succession from multiple hosts, overwhelming the server that tries to respond to them. Another example is the "ping of death," in which a single ping command with a very large payload is sent to a server; the payload overflows the memory space allocated for ping packets and corrupts other parts of the server's memory.

To avoid wasted time because of systems that don't respond to ping, find a few Internet sites (universities are a good bet) that do respond, then use those sites for your occasional ping tests.

Notice now the parts of the ping output from the listing shown previously. They include:

+   - The number of bytes sent in the packet. You can change this using a parameter of ping, should you ever need to.
+   - The host name (if you included one) and IP address of the host you are pinging.
+   - A sequence number, starting with 0. The number counts up by 1 until you press Ctrl+c to end ping.
+   - The Time to Live (ttl) of the ping packet. This is the number of routers that the packet can pass through before being discarded. The default here—224—is quite high, indicating that you really want to reach the host.