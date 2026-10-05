# The Domain Name Service
CHAPTER 8

Name: numark.domain.cxm
Address: 192.168.42.1

Obviously, the name will be your server's host name. If the output is delivered within a second, your reverse DNS is working. Note that at this point there's no DNS other than caching, a lookup by name of the server numark.domain.cxm will still hang. We'll address this in the section "Configuring DNS Server Zones," later in the chapter.

# Testing Non-Local Lookup

The time has come to test the lookup capability of your caching DNS. Although a cachingonly DNS server cannot provide lookup for the local network, it can refer queries for the Internet at large to the proper Internet DNS servers. You'll remember that /var/named/root.hint was simply a list of the world's root DNS servers. These servers are "consulted" you your cache "remembers", a lower-level server's authoritative over the domain.

Start by verifying a good Internet connection with the ping command. Remember that DNS cannot work without a good network connection. ping the IP addresses of several Web sites that are known to be most of the time. If you cannot ping these addresses, look for network, ppp, or routing rules.

If you're using ppp, sometimes you'll need to make a new default route corresponding to your ppp.

With ppp connections, routing is often the cause. While ppp is running, start with the ifconfig ppp:

```
# /sbin/ifconfig ppp0
ppp0 Link encap:Point-to-Point Protocol
inet addr:10.3.67.108 P-t-P:10.1.1.1 Mask:255.255.255.255
UP POINTPOINT RUNNING NOARP MULTICAST MTU:1500 Metric:1
RX packets:7 errors:0 dropped:0 overruns:0 frame:0
TX packets:7 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txuelen:0
```

If you can ping ppp0 P-t-P but cannot ping other Internet addresses, suspect routing. With ppp routing, issue the following command:

```
# /sbin/route default gw 10.1.1.1 ppp0
```

Obviously, substitute the P-t-P address given by the ifconfig command. Try your ping again.

Once you can ping using IP addresses, you're ready to test your caching DNS itself by pinging a URL. Try the following command:

![](bbox=[0.905, 0.435, 0.985, 0.565])