```
www.handsonhistory.com ping statistics
4 packets transmitted, 3 packets received, 25% packet loss
round-trip min/avg/max/mdev = 116.816/119.277/120.807/1.719 ms
```

Press [Ctrl]+C to end the ping command. The previous lines show the responses from www.handsonhistory.com. It sent back packets from the IP address 198.60.22.8 in response to each one it received. You can see the sequence of packets (*c*mp*seq*) and the time it took for each response in milliseconds. If you receive packets in return, you will know two things: first, that your connection is working, and second, that your name to address translation from the DNS addresses in *etc/resolv.conf* is working.

# ## Checking the Default Route

After starting a dial-up connection, check that the default route is set using `route -n`, as shown in the following example:

```
# /sbin/route -n
Kernel IP routing table
Destination Gateway Genmask Flags Metric Ref Use Iface
198.62.1.1 0.0.0.0 255.255.255.255 UH 0 0 0 ppp0
10.0.0.0 0.0.0.0 255.0.0.0 U 0 0 0 eth0
169.254.0.0 0.0.0.0 255.255.0.0 U 0 0 0 eth0
127.0.0.0 0.0.0.0 255.0.0.0 U 0 0 0 lo
0.0.0.0 198.62.1.1 0.0.0.0 UG 0 0 0 ppp0
```

This shows that the gateway was set to the remote PPP server (198.62.1.1), as well as showing the other interfaces running on my computer. There are two lines *entries*. The first shows the destination as a host (H). The second shows the destination as a gateway (G). The address entry 169.254.0.0 indicates that all addresses for subnetwork 169.254 should be directed to the local network. Microsoft clients that can't get an IP address via DHCP or other means will assign themselves IP addresses in this range. All addresses that can't be resolved on the local LAN are directed to the gateway address.

# ## Checking That The Name Servers Are Set

If you are able to ping a remote computer by IP address but are not able to resolve any addresses, your DNS servers may not be set correctly. As *root* user from a Terminal window, open the *etc/resolv.conf* file and check that there are lines identifying one or more DNS servers in this file. These should be supplied to you by your ISP, unless you run your own DNS server.

Try using the ping command to make sure that the name servers are live.

> NOTE When you connect to your ISP using DHCP, it's possible that during the connection process, new name server information will appear in your *etc/resolv.conf* file and old entries will be lost. This can be a problem if you are relying on your own server for providing DNS service and its entry is erased.