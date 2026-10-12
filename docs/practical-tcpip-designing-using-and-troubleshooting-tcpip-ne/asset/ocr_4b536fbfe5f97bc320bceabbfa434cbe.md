But note that we said “as far as its IP layer is concerned” up above. Higher-level protocols – such as TCP, UDP, or application-level protocols such as HTTP, all of which we discuss in Part 2 of the book – are likely to notice that there is a problem and report the error. In the example above it was the Windows *ping* application that noticed it didn’t get any responses and reported it

+   6. from the command line run `“telnet 1.2.3.4”`

+   7. After a long wait (800 seconds on Linux) Linux says “telnet: Unable to connect to remote host: No route to host.” (This is a misleading message because it has nothing to do with routing as such: it just means it can’t contact the destination.) NT says “Connect failed”.
+   So while the IP layer isn’t reporting any error, the application layer is. The low-level routing components on your machine just didn’t notice anything wrong at all. (The human equivalent is the infuriating “more than my job’s worth” messenger boy: “I was told I should put all letters for Bloggs Corp. into that letter-box. It’s not my fault that someone set fire to the letter-box and flames were coming out of it when I dropped the letters in.”)

# The default gateway has no valid route to the destination

+   1. connect the same machine to a router
+   2. configure the router’s IP address =10.1.1.163, netmask =255.255.255.0, no default gateway
+   3. `ping 1.2.3.4`
+   4. Linux **ping** reports “Network is unreachable.” Windows **ping** reports “Destination host unreachable”
+   5. `telnet 1.2.3.4`

The default gateway can’t send because it doesn’t know of any appropriate route, so it reports this immediately using ICMP, which we see with **tcpdump**

```
10.1.1.163 > 10.1.1.59: icmp: host 1.2.3.4 unreachable
```

and the application *immediately* gives the following error and terminates:

```
telnet 1.2.3.4 Unable to connect to remote host: No route to host
```

When a router reports an “ICMP host unreachable” error, it’s final: it can’t reach it now and with its current configuration it never will be able to in the future; so there’s no point waiting, and the connection can be terminated immediately. On the other hand, when the routing tables indicate there is a route to the destination but packets are just not getting through, this could be caused by temporary network problems or slowness on the Internet, so applications wait for a considerable period before timing out with an error.

> **Exercise:** telnet to a non-existent host that ought to be on the directly connected LAN, and see how long it takes to report an error, e.g.
> ```
> telnet 10.1.1.123
> ```
> What happens with
> ```
> ping 10.1.1.123
> ```
> What does **tcpdump** show if you traceroute to a non-existent host?