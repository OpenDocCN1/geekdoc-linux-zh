# 468 Part III ♦ Choosing and Installing a Linux Distribution

As with the input commands, the firewall accepts outgoing packets that come from any of the local firewall interfaces (127.0.0.1, 10.0.0.1, and 323.45.67.89). It also accepts outgoing packets associated with destinations on the private LAN (10.0.0.0/24 and 10.0.0.255).

+   6. This list of commands defines what packets originated from the Internet are allowed into the firewall. For packets attempting to enter your computer from the Internet, you want to be more restrictive, in allowing only for services you want to provide. Here are some examples of specific rules you might want to allow for your server:

```
@ INPUT -A INPUT -p tcp -s eth 0 -destination-port 21 -j ACCEPT
@ INPUT -A INPUT -p tcp -s eth 0 -destination-port 22 -j ACCEPT
@ INPUT -A INPUT -p tcp -s eth 0 -destination-port 80 -j ACCEPT
@ INPUT -A INPUT -p tcp -s eth 0 -destination-port 113 -j ACCEPT
@ INPUT -A INPUT -p udp -s eth 0 -destination-port 2074 -j ACCEPT
@ INPUT -A INPUT -p udp -s eth 0 -destination-port 4000 -j ACCEPT
```

The first four lines open ports for the TCP services you want to provide to anyone on the Internet: for FTP service (--port 21), secure shell (22), Web service (80), and IDENTD authentication (113), the last of which might be necessary for protocols such as IRC.

> You must ensure that the services on the ports to which you are allowing access are properly configured before you allow packets to be accepted. In other words, don't open port 80 until you have a Web server configured or port 53 before you have a DNS server configured.

The last three lines define the ports where connections are accepted from the Internet. This example assumes that DNS service (---port 53) is configured on the computer. It also illustrates lines that accept requests for two other ports: Port 2074 is needed by some multimedia applications the users on your LAN might want to use, and port 4000 is used by the ICQ protocol (for online chats).

At this point you can run iptables -l to see your new set of rules. If you have a connection to the computer from your LAN, you can try to ping the computer from the LAN. You can also try configuring different services and accessing them from your network interfaces.

With this part of the procedure completed, your new firewall rules are built into the Linux kernel but do not exist anywhere in a configuration file. Unless you save the rules, they will be gone next time you reboot your computer. The following discusses saving your firewall settings so you can use them permanently.

![](bbox=[0.12, 0.476, 0.196, 0.546])