# EXERCISE 8.1 (continued)

+   9. Bring the local Ethernet connection back up by typing `ifconfig eth0 up address netmask mask`, where *address* is the original IP address and *mask* is the original netmask, both as identified in step 4.
+   10. Repeat steps 4–6. Note that the `ifconfig` command automatically added back your local network to the routing table but that the default route is still missing. As a result, you can't contact any systems that are located off the local network. If your DNS server is such a system, this means your ability to contact even local machines by name may be impaired as well.
+   11. Restore the default route by typing `route add default gw gateway`, where *gateway* is the router address you identified in step 5.
+   12. Repeat steps 4–6. If your network configuration is typical, all connectivity should be restored. (Some more exotic systems may still be lacking certain routes.)

![](bbox=[0.13, 0.46, 0.38, 0.48])

# Using PPP with DSL

Broadband users, and particularly those with Digital Subscriber Line (DSL) connections, sometimes have to use a variant of PPP to make their connections. PPP is a login-based way to access the Internet—you use a PPP utility to initiate a connection to a remote computer, which includes an exchange of a username and a password. A decade ago, PPP was used in dial-up Internet access (and it’s still used in this capacity), but some DSL providers have adapted PPP for their own purposes. In the case of DSL, this configuration method is called PPP over Ethernet (PPPoE).

In many cases, the simplest way to use a PPPoE configuration is to purchase a broadband router. This device attaches to the DSL modem and makes the PPPoE connection. The broadband router then works just like an ordinary Ethernet or Wi-Fi router, as far as your local computers are concerned, so you can configure Linux as you would on any other local network.

If you must connect a Linux system directly to a DSL network that uses PPPoE, you must use a Linux PPPoE client. Most Linux distributions ship with such clients; but configuration details vary from one distribution to another. Your best bet is to look for your distribution’s GUI network configuration tool; chances are, you’ll be able to find a set of options that are clearly labeled as applying to DSL or PPPoE.