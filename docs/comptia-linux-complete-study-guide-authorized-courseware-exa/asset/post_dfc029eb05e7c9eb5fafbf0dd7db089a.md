
# Diagnosing Network Connections

Network configuration is a complex topic, and unfortunately, things don’t always work as planned. Fortunately, there are a few commands you can use to help diagnose a problem. Five of these are ping, traceroute, tracepath, netstat, and tcpdump. Each of these commands exercises the network in a particular way and provides information that can help you track down the source of a problem. You can also use some common network programs that aren’t primarily debugging tools in your debugging efforts.

## Testing Basic Connectivity

The most basic network test is the ping command, which sends a simple ICMP packet to the system you name (via IP address or hostname) and waits for a reply. In Linux, ping continues sending packets once every second or so until you interrupt it with a Ctrl+C key-stroke. (You can instead specify a limited number of tests via the -c num option.) Here’s an example of its output:

```
$ ping -c 4 speaker
PING speaker (192.168.1.1) 56(84) bytes of data.
64 bytes from speaker.example.com (192.168.1.1): icmp_seq=1 ttl=64 time=0.194ms
64 bytes from speaker.example.com (192.168.1.1): icmp_seq=2 ttl=64 time=0.203ms
64 bytes from speaker.example.com (192.168.1.1): icmp_seq=3 ttl=64 time=0.229ms
64 bytes from speaker.example.com (192.168.1.1): icmp_seq=4 ttl=64 time=0.217ms
--- speaker ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3002ms
rtt min/avg/max/mdev = 0.194/0.210/0.229/0.022 ms
```

This command sent four packets and waited for their return, which occurred quite quickly (in an average of 0.210ms) because the target system was on the local network. By pinging systems on both local and remote networks, you can isolate where a network problem occurs. For instance, if you can ping local systems but not remote systems, the problem is most probably in your router configuration. If you can ping by IP address but not by name, the problem is with your DNS configuration.

## Tracing a Route

A step up from ping is the traceroute command, which sends a series of three test packets to each computer between your system and a specified target system. The result looks something like this:

```
$ traceroute -n 10.1.0.43
traceroute to 10.1.0.43 (10.1.0.43), 30 hops max, 52 byte packets
1   192.168.1.254     1.021 ms     36.519 ms     0.971 ms
2   10.10.88.1      17.250 ms      9.959 ms      9.637 ms
3   10.9.8.173      8.799 ms      19.501 ms     10.884 ms
4   10.9.8.133      21.059 ms      9.231 ms     103.068 ms
5   10.9.14.9       8.554 ms      12.982 ms     10.029 ms
6   10.1.0.44       10.273 ms      9.987 ms     11.215 ms
7   10.1.0.43       16.360 ms       *     8.102 ms
```

The -n option to this command tells it to display target computers’ IP addresses rather than their hostnames. This can speed up the process a bit, particularly if you’re having DNS problems, and it can sometimes make the output easier to read—but you may want to know the hostnames of problem systems because that can help you pinpoint who’s responsible for a problem.

This sample output shows a great deal of variability in response times. The first hop, to 192.168.1.254, is purely local; this router responded in 1.021, 36.519, and 0.971 milliseconds (ms) to its three probes. (Presumably the second probe caught the system while it was busy with something else.) Probes of most subsequent systems are in the 8–20ms range, although one is at 103.068ms. The final system has only two times; the middle probe never returned, as the asterisk (*) on this line indicates.

Using traceroute, you can localize problems in network connectivity. Highly variable times and missing times can indicate a router that’s overloaded or that has an unreliable link to the previous system on the list. If you see a dramatic jump in times, it typically means that the physical distance between two routers is great. This is common in intercontinental links. Such jumps don’t necessarily signify a problem unless the two systems are close enough that a huge jump isn’t expected.

What can you do with the traceroute output? Most immediately, traceroute is helpful in determining whether a problem in network connectivity exists in a network for which you’re responsible. For instance, the variability in the first hop of the preceding example could indicate a problem on the local network, but the lost packet associated with the final destination most likely is not a local problem. If the trouble link is within your jurisdiction, you can check the status of the problem system, nearby systems, and the network segment in general.

![Image](img/f339a9f48c4b443e61c74acb4c9c3da4_472_0.png)

Some routers are configured in such a way that traceroute isn’t a useful tool; these routers block all traceroute data, either to themselves only or for all packets that pass through them. If your traceroute output contains one or two lines of all asterisks but everything else seems OK, chances are you’ve run into such a system. If you see nothing but asterisks after a certain router but diagnostic tools such as ping still work, a router is probably blocking all traceroute operations.

The tracepath program is an alternative to traceroute. In basic operation, it’s similar, although it produces one line of output for each test packet and so yields longer outputs than traceroute. There are also fewer tracepath options than there are traceroute options.

## Checking Network Status

Another useful diagnostic tool is `netstat`. This is something of a Swiss Army knife of network tools because it can be used in place of several others, depending on the parameters it’s passed. It can also return information that’s not easily obtained in other ways. Some examples include the following:

- **Interface information** Pass `netstat` the `--interface` or `-i` parameter to obtain information about your network interfaces similar to what `ifconfig` returns. (Some versions of `netstat` return information in the same format, but others display the information differently.)
- **Routing information** You can use the `--route` or `-r` parameter to obtain a routing table listing similar to what the `route` command displays.
- **Masquerade information** Pass `netstat` the `--masquerade` or `-M` parameter to obtain information about connections mediated by Linux’s NAT features, which often go by the name *IP masquerading*. NAT enables a Linux router to “hide” a network behind a single IP address. This can be a good way to stretch limited IPv4 addresses.
- **Program use** Some versions of `netstat` support the `--program` (or `-p`) parameter, which attempts to provide information about the programs that are using network connections. This attempt isn’t always successful, but it often is, so you can see what programs are making outside connections.
- **Open ports** When used with various other parameters, or without any parameters at all, `netstat` returns information about open ports and the systems to which they connect.
- **All connections** The `-a` option is used in conjunction with others. It causes `netstat` to display information about the ports that server programs open to listen for network connections, in addition to already-open connections. This use of `netstat` is described in more detail in Chapter 10, “Securing Your System.”

> Keep in mind that `netstat` is a very powerful tool, and its options and output aren’t entirely consistent from one distribution to another. You may want to peruse its man page and experiment with it to learn what it can do.

## Examining Raw Network Traffic

One advanced network troubleshooting tool is `tcpdump`. This utility is a *packet sniffer*, which is a program that can intercept network packets and log them or display them on the screen. Packet sniffers can be useful diagnostic tools because they enable you to verify that a computer is actually receiving data from other computers. They also enable you to examine the data in its raw form, which can be useful if you understand enough of the protocol’s implementation details to spot problems.
