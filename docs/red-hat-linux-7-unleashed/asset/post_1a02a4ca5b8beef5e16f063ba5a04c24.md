
## Novell Support

There is support built in for the Novell SPX and IPX protocols. The interface setup screen in *linuxconf* is used for configuring information required to access networked resources on a Novell network using the IPX/SPX protocols. The Enable button on the introductory screen must be pressed in order to use this option. The subsequent information required on the Adapter 1 and Internal Net tabs can be obtained by your Novell network administrator.

You can (as root) control what services are started or not run during bootup by using the *ntsysv* command. However, you should know that you'll shut off all networking services unless you run *xinetd*. A much better approach is to edit its configuration files, found under the */etc* directory, and the */etc/xinetd.d* directory. For example, here is the default *telnet* control file under */etc/xinetd.d* directory:

```
# default: on
# description: The telnet server serves telnet sessions; it uses \
#            unencrypted username/password pairs for authentication.

service telnet
{
    disable = no
    flags       = REUSE
    socket_type = stream
    wait        = no
    user        = root
    server      = /usr/sbin/in.telnetd
    log_on_failure  += USERID
}
```

As you can see, the default state for *telnet* access is enabled with Red Hat Linux. Your job as a system administrator will be to decide what services to provide on your system.

## TCP/IP Troubleshooting Tools

Problems rarely appear once a TCP/IP network is configured. However, networking equipment fails, lines go down, and cables get disconnected. Also, problems can arise during the initial configuration of a networked host.

Linux has three basic network troubleshooting tools. Two of them, **ping** and **traceroute**, are concerned with the capability of a host to reach another, while the third one, `tcpdump`, is useful for analyzing the flow of traffic in a network.

### ping

The most basic network troubleshooting tool is the **ping** program. Named after the pinging sound made by submarine sonars, **ping** sends out packets to another host and waits for that host to reply to them. **ping** uses ICMP (Internet Control Message Protocol), a protocol that runs over IP and is designed for control messages used for things such as routing and reachability information.

The most common way of using **ping** is to pass it a hostname or address:

```
% ping server.company.com
PING server.company.com (10.0.1.10): 56 data bytes
64 bytes from 10.0.1.10: icmp_seq=0 ttl=245 time=83.239 ms
64 bytes from 10.0.1.10: icmp_seq=1 ttl=245 time=80.008 ms
64 bytes from 10.0.1.10: icmp_seq=2 ttl=245 time=82.994 ms
64 bytes from 10.0.1.10: icmp_seq=3 ttl=245 time=81.635 ms
^C
--- server.company.com ping statistics ---
4 packets transmitted, 4 packets received, 0% packet loss
round-trip min/avg/max = 80.008/82.169/83.239 ms
```

In this case, **ping** pings the target host one time per second, until you press Ctrl+C. At that moment, it prints out the statistics for the run. In the statistics, aside from the number of packets transmitted and received, you can see the minimum, average, and maximum round-trip times, which will help you find out how congested the path to the destination host is at the moment.

**ping** has many options. Here are the most commonly used:

| Option | Function |
| :--- | :--- |
| -c count | Only sends *count* number of packets instead of pinging forever. |
| -n | **ping** displays numeric addresses instead of hostnames. Useful when you can't get to the DNS server or when DNS queries take too long. |
| -r | Record route. Sends an option in every packet that instructs every host between the source and the target to store its IP address in the packet. This way you can see which hosts a packet is going through. However, the packet size is limited to nine hosts. Some systems disregard this option. Because of this, it is better to use *traceroute*. |
| -q | Quiet output. Outputs just the final statistics. |
| -v | Verbose. Displays all packets received, not just *ping* responses. |

When troubleshooting network problems, you should first ping the IP address of the source host itself. This verifies that the originating network interface is set up correctly. After that, you should try pinging your default gateway. Your default gateway’s gateway (the next hop out), and so on, until you reach the destination host. That way you can easily isolate where a problem lies. However, once you’ve verified that you can get to the default gateway, it is better to use the **traceroute** program (which is described in the following section) to automate the process.

> **Note**
>
> All TCP/IP packets have a field called Time-To-Live, or TTL. This field is decremented once by each router on the network. The packet is discarded the moment it reaches `0`. Whereas `ping` uses a default TTL of `255` (the maximum value), many programs such as `telnet` and `ftp` use a smaller TTL (usually `30` or `60`). That means that you might be able to `ping` a host, but not `telnet` or `ftp` into it. You may use the `-t ttl` option to `ping` to set the TTL of the packets it outputs.

### traceroute

The `traceroute` program is the workhorse of TCP/IP troubleshooting. It sends out UDP packets with progressively larger TTLs and detects the ICMP responses sent by gateways when they drop the packets. In the end, this maps out the route a packet takes when going from the source host to the target host.

This is how it works: `traceroute` starts by sending out a packet with a TTL of `1`. The packet gets to a gateway, which can be the target host or not. If it is the target host, the gateway sends a response packet. If it isn’t the target host, the gateway decrements the TTL. Since the TTL is now `0`, the gateway drops the packet and sends back a packet indicating this. Whatever happens, `traceroute` detects the reply packet. If it has reached the target host, its job is finished. If not (it received notification that the packet was dropped, for instance), it increments the TTL by `1` (its new value is `2`) and sends out another packet. This time the first gateway decrements the TTL (to `1`) and passes it through to the next gateway. This gateway does the same thing: determines whether it’s the destination host and decrements the TTL. This goes on until either you reach the target host or you reach the maximum TTL value (which is `30` by default, but can be changed with the `-m max_ttl` option).

`traceroute` sends three packets with each TTL and reports the round-trip time taken by each packet. This is useful for detecting network bottlenecks.

tracroute is usually used the same way as ping—by giving it a destination address. Listing 20.1 shows an example of the output from tracroute.

## **LISTING 20.1 Sample Output from tracroute**

```
mario@chaos:~$ ll /usr/sbin/tracroute www.umbral.com
tracroute to xnya.umbral.com (207.87.10.30), 30 hops max, 40 byte packets
1: master.spin.com.mx (200.13.60.123) 120.75 ms 126.74 ms 100.533 ms
2: octopus.spin.com.mx (200.13.61.32) 110.042 ms 104.654 ms 99.599 ms
3: 200.33.216.161 (200.33.216.161) 119.589 ms 105.897 ms 109.603 ms
4: rri1.memxfd.aventel.net.mx (200.33.209.1) 131.555 ms 112.566 ms 107.6103.6 ms
5: bordercore2-hss10-0Dallas.cw.net (166.48.77.249) 159.54 ms 155.378 ms 159.590 ms
6: core0.Dallas.cw.net (200.70.9.60) 159.493 ms 156.364 ms 159.620 ms
7: dfdz-core2-s1-0.atlas.digex.net (165.117.59.13) 169.595 ms 156.924 ms 149.620 ms
8: lax1-core1-s8-0.0.atlas.digex.net (165.117.58.25) 199.497 ms 194.896 ms 189.621 ms
9: sjc4-core2-s5-0.0.atlas.digex.net (165.117.53.74) 199.489 ms 199.460 ms
==> sjc4-core2-s5-1-0.atlas.digex.net [165.117.58.110] 191.825 ms
== sjc4-core2-s5-0-0.atlas.digex.net [165.117.53.74] 210.25 ms
10: sjc4-core6-posi-1.atlas.digex.net (165.117.59.69) 201.91 ms 196.195 ms 199.584 ms
11: sjc4-wscore-p2-0.wscq.digex.net (199.125.178.37) 360.488 ms 366.267 ms 199.461 ms
12: sjc4-wsc0e4-fa1-0.wscq.digex.net (199.125.178.28) 582.272 ms 207.535 ms 198.275 ms
13: xnya.umbral.com (207.87.10.30) 209.457 ms 3076.14 ms *
```

tracroute can give you quite a bit of information if you know how to look for it. For example, you can see a few things in Listing 20.1:

- www.umbral.com is actually an alias for xnya.umbral.com. tracroute always does a reverse DNS lookup and reports the official hostname of the host it’s tracing.
- xnya.umbral.com is connected to the Internet through a service provider whose domain is digex.net (probably an ISP called Digex). (Lines 7–12 are all in the IP networks belonging to the domain of the last gateway.)
- You are connected to the Internet through an ISP called Spin, which is in Mexico. (Lines 1 and 2 are the first gateway. The domain ends with .mx.)
- The digex hosts that appear on line 9 are actually several hosts with the same IP address. This is done for redundancy.
- There seems to be some kind of bottleneck between hosts 10, 11, and 12. Notice how the response time, after slowly growing steadily until line 9, suddenly jumps from about 200 milliseconds to more than 300, and then to more than 500. This might be a temporary bottleneck (caused simply by the traffic load at the moment or it may be a continuous problem, caused perhaps by a physical media problem or not enough capacity in the link.)
