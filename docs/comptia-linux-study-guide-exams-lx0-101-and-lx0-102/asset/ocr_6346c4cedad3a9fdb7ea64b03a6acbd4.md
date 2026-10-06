# Diagnosing Network Connections 411

you can't contact any systems that are located off the local network. If your DNS server is such a system, this means your ability to connect even local machines by name may be impaired as well.

+   11. Restore the default route by typing route default gw gateway, where gateway is the router you identified in step 5.

+   12. Repeat steps 4–6. If your network configuration is typical, all connectivity should be restored. (Some more exotic systems may still be lacking routes.)

![](bbox=[0.125, 0.296, 0.175, 0.335])

# Real World Scenario Using PPP with DSL

Broadband users, and particularly those with Digital Subscriber Line (DSL) connections, sometimes have to use a variant of PPP to make their connections. PPP is a login-based way to access the Internet–you use PPP to initiate a connection to a remote computer, which includes an exchange of username and a password. De decade ago, PPP was used in dial-up access (and it's still used in this capacity), but some DSL providers adopted PPP for their own purposes. In the case of DSL, this configuration method is called PPP over Ethernet (PPPoE).

In many cases, the simplest way to use a PPPoE configuration is to purchase a broadband router. This device attaches to the DSL modem and makes the PPPoE connection. The broadband router works just like an ordinary Ethernet or Wi-Fi router, as far as the local computers are concerned, so you configure Linux as you would on any other local network.

If you must connect a Linux system directly to a DSL network that uses PPPoE, you must use a Linux PPP client. Most Linux distributions ship with such clients, but configuration details vary from one distribution to another. Your best bet is to look for your distribution's GUI network configuration tool; chances are, you'll be able to find a set of options that are clearly labeled as applying to DSL or PPPoE.

# Diagnosing Network Connections

Network configuration is a complex task, and unfortunately, things don't always work as planned. Five of these are ping, traceroute, tracepath, netstat, and tcpdump. Each of these exercises the network in a particular way and provides information that can help you track the source of a problem. You can also use some common network programs that aren't primarily debugging tools in your debugging efforts.