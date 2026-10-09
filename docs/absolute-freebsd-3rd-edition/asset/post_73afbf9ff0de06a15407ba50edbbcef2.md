
translation slow down the output, it can cause ambiguous output. Finally, the -f inet option tells netstat(8) to worry only about IPv4 network connections, while -f inet6 addresses IPv6. Here's matching netstat output from the same machine we just ran sockstat(1) on:

```
# netstat -na -f inet
Active Internet connections (including servers)
Proto Recv-Q Send-Q  Local Address          Foreign Address        (state)
tcp4   0      0      203.0.113.43.22        24.192.127.92.62937    ESTABLISHED
tcp4   0      0      *.25                   *.*                    LISTEN
tcp4   0      0      *.23                   *.*                    LISTEN
tcp4   0      0      *.80                   *.*                    LISTEN
tcp4   0      0      *.22                   *.*                    LISTEN
tcp4   0      0      203.0.113.8.53         *.*                    LISTEN
udp4   0      0      203.0.113.8.53         *.*
```

Here, we get no idea of what program is attached to any port. The first entry in each column is the transport protocol used by the socket—mostly TCP, but the last line shows UDP.

The `Recv-Q` and `Send-Q` columns show the number of bytes waiting to be handled by this connection. If you see nonzero `Recv-Q` numbers for some connection most of the time, you know that the program listening on that port can’t process incoming data quickly enough to keep up with the network stack. Similarly, if the `Send-Q` column keeps having nonzero entries, you know that either the network or the remote system can’t accept data as quickly as you’re sending it. Occasional queued packets are normal, but if they don’t go away, you might want to investigate why things are slow. You must watch your own system to learn what’s normal.

The `Local Address` is, as you might guess, the IP address and network port number on the local system that the network connection is listening on. The network port appears at the end of the entry and is separated from the IP address by a dot. For example, 203.0.113.43.22 is the IP address 203.0.113.43, port 22. If the entry is an asterisk followed by a period and a port number, that means that the system is listening on that port on all available IP addresses. The system is ready to accept a connection on that port.

The `Foreign Address` column shows the remote address and port number of any connection.

Finally, the (state) column shows the status of the TCP handshake. You don't need to know all of the possible TCP connection states, so long as you learn what's normal. `ESTABLISHED` means that a connection exists and that data is probably flowing. `LAST_ACK`, `FIN_WAIT_1`, and `FIN_WAIT_2` mean that the connection is being closed. `SYN_RCVD`, `ACK`, and `SYN+ACK` are all parts of connection creation (the three-way handshake from Chapter 7). `LISTEN` indicates that the port is ready for incoming connections. In the preceding example, one TCP connection is running and four are ready to accept clients. As UDP is stateless, those connections list no state information.

By reading this output and combining it with information provided by sockstat(1), you can learn exactly which programs are behaving well and which are suffering bottlenecks.

If you're not interested in listening sockets but only those with active connections, use netstat(8)'s -b option instead of -a. Running netstat -nb -f inet displays only connections with foreign systems.

You can also use netstat -T to display TCP retransmits and out-of-order packets on individual connections. Retransmits and misordered packets are symptoms of dropped packets.

## Network Capacity in the Kernel

The FreeBSD kernel handles network memory by using mbufs. An mbuf is a chunk of kernel memory used for networking. You'll keep tripping across mentions of mbufs throughout the FreeBSD network stack documentation, so it's important to have at least a vague idea of them.

FreeBSD automatically allocates network capacity at boot time based on the amount of physical RAM in the system. We assume that if you have a system with 64GB RAM, you want to use more memory for networking than on a little box with 1GB RAM. View how FreeBSD uses its resources with netstat -s and netstat -m. Let's look at the shortest one first.

To get a generic view of kernel memory used for networking, run netstat -m. The output can be divided into two general categories: how much is used and how many requests failed. The following output is trimmed to include only a few examples of these, but they all follow the same general format:

```
# netstat -m
---snip--
132/372/404/25600 mbuf clusters in use (current/cache/total/max)
---snip--
0/0/0 requests for mbufs 0 denied (mbufs/clusters/mbuf+clusters)
---snip--
```

Here we see how many mbuf clusters are used. You’d probably guess that these are related to mbufs, and you’d be right. You don’t have to know exactly what mbuf clusters are; the important thing is that you know how many you can allocate and can see that you’re under that limit.

Similarly, we can see how many different requests for mbufs the kernel has denied. This system hasn’t rejected any requests for mbufs, which means that we aren’t having performance problems due to memory shortages. If your system starts rejecting mbuf requests because it’s out of memory, you’re in trouble. See “Optimizing Network Performance” next.

While netstat -m produces a dozen lines of output, netstat -s runs for pages and pages. It provides per-protocol performance statistics. Much like netstat -n, you can break up these statistics into categories of how much was done and how many problems you had. Run both of these commands occasionally on your systems and review the results so you know what passes for normal on your servers and can recognize abnormal numbers when you have problems.

## Optimizing Network Performance

Now that you can see what’s going on, how could you improve FreeBSD’s network performance? There’s a simple rule of thumb when considering optimizing: don’t. Network performance is generally limited only by your hardware. Many applications can’t process data as quickly as your network can provide. If you think that you need to optimize your performance, you’re probably looking in the wrong spot. Check Chapter 21 for hints on investigating performance bottlenecks.

Generally speaking, network performance should be adjusted only when you experience network problems. This means that you should have output from netstat -m or netstat -s indicating that the kernel is having resource problems. If the kernel starts denying requests for resources or dropping connection requests, look at the hints in this section. If you have issues or if you think you should be getting better performance, look at the hardware first.

### Optimizing Network Hardware

Not all network hardware is created equal. While anyone in IT hears this frequently, FreeBSD’s open nature makes this obvious. For example, here’s a comment from the source code of the rl(4) network card driver:

> The RealTek 8139 PCI NIC redefines the meaning of ‘low end.’ This is probably the worst PCI ethernet controller ever made, with the possible exception of the FEAST chip made by SMC. The 8139 supports bus-master DMA, but it has a terrible interface that nullifies any performance gains that bus-master DMA usually offers.

This can be summarized as, “This card sucks and blows at the same time. Buy another card.” While this is the most vitriolic comment that I’ve seen in the FreeBSD source code, and this particular hardware is very hard to find today, the drivers for certain other cards say the same thing in a more polite manner. Optimizing network performance with low-end hardware is like putting a high-performance racing transmission in your 1974 Gremlin. Replacing your cheap network card will probably fix your problems. Generally speaking, Intel makes decent network cards; they maintain a FreeBSD driver for their wired network cards and provide support so that the FreeBSD community can help maintain the drivers. (Wireless cards are another story.) Similarly, many companies that build server-grade machines make a point of using server-grade network cards. Some companies provide a FreeBSD driver but do not provide documentation for their hardware. This means that the driver probably works, but you’re entirely dependent upon the
