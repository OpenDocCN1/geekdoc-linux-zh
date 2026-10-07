# Figure 4.10 Displaying the Host Routing Table

```
root@Forensic3:#
root@Forensic3:# -netstat -rn
Kernel IP routing table
Destination     Gateway      Genmask      Flags  MSS Window  irtt Iface
192.168.10.10   0.0.0.0      255.255.255.0   U       0             0       0 eth0
0.0.0.0         192.168.10.100  0.0.0.0        UG      0             0       0 eth0
root@Forensic3:# 
```

As you can see from Figure 4.10, where the route is headed and which gateway is being used. In the event that no gateway is used, an asterisk (*) will appear in the column. The next column shows the “generality” of the route, or in other words, the network mask for that particular route. The next column displays the flags that can be set. The flag breakdown is:

+   - Gateway
- The interface being used is Up
- Only a single Host can be reached through the route, like the loopback
- The route has been Dynamically created
- Modified by an Internet Control Message Protocol (ICMP) redirect
- ! The route is a reject, and the packets will be dropped

# Running Processes

It is important to know what is running on the host you are analyzing. This can be accomplished by a few different commands. For the purposes of this book, I only cover “ps aux” and “top.” (See Figure 4.11.)