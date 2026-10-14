![](bbox=[0.07, 0.07, 0.92, 0.44])

# Figure 15-13 IP masquerading

firewall because a remote computer cannot connect to a client within a masqueraded LAN. If you configure the router carefully, IP masquerading effectively hides your entire network.

Setting up IP masquerading requires a rule that says in effect, “Any network traffic coming from this network should be masqueraded.” Suppose you have a LAN (using device eth0) with the network address 192.168.100.0 that you connect to the Internet through a cable modem. Using the following command on the server would cause all network traffic from the internal network to be masqueraded; all clients on the LAN would then be able to access the Internet (though the ISP would see all traffic as coming from the gateway system). The nat table (per the -t option) refers to the network address translation table; the -A POSTROUTING option appends this rule to the list of rules used after other routing decisions have been made.

```
# iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

# Graphical Firewall Configuration Utilities

Although the syntax of the iptables command is straightforward once you are accustomed to it, a graphical utility can still be very helpful in setting up a Linux firewall.

![](bbox=[0.09, 0.92, 0.18, 1.0])

> You need to understand how IP tables and the networking protocols operate before a graphical utility will be of much help in configuring a secure firewall.

Red Hat Linux and Fedora, like many other Linux distributions, include basic firewall configuration tools to help new users give their systems some level of protection. When you install Red Hat Linux or Fedora, you answer basic questions about your network security. These questions are posed using the system-config-securitylevel program, which you can