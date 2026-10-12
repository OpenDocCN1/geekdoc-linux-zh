# **3.7 Lab – building the simplest possible inter-network (2)**

# **3. Setting the network parameters**

+   1.  configuring Alice and Bob is straightforward – we’ve explained how to set the IP address and netmask, and the default gateway. Alice’s default gateway is 10.1.1.163 – the left side of Rupert – so any packets Alice wants to send outside her network, e.g. to Bob, are passed to 10.1.1.163 for forwarding. Similarly, Bob’s default gateway is 10.2.2.14
+   2.  Rupert has two network cards. This is a new feature: we explain below how to configure them
+   3.  Rupert has no default gateway set, and doesn’t need one, because he is directly connected to all the networks in our tiny inter-network, and can therefore send packets to any machine he needs to.

# **Configuring multiple network cards**

**Linux:** “`ifconfig -a`” will show you whether you have multiple interfaces, and what their names are. To set parameters for a particular interface, use that interface’s name in the command (as you have done already, although you always used *eth0*). For example, to set the parameters for Rupert:

```
```
ifconfig eth0 10.1.1.163  netmask 255.255.255.0 up
ifconfig eth1 10.2.2.14   netmask 255.255.255.0 up
```
```

We use the keyword “**up**” in the commands to make sure the interfaces are active, not just present. To make the parameters permanent, you have to store them in the appropriate configuration file: see Appendix 6.

**Windows:** configuring multiple network cards is even more straightforward – in the *Control Panel > Network > Protocols > TCP/IP Properties* window, select the interface you want to set from the pull-down selection list (Figure 3.15).

![](bbox=[0.32, 0.63, 0.7, 0.74])

**Figure 3.15 Selecting an interface**

When you are using multiple network cards on NT, you have to reboot for the changes to take effect. As usual, use **ifconfig** to check the settings in effect after you’ve made the changes and rebooted.

> Tip: in real life, where possible we keep the last byte of all the IP addresses on a router the same, just to make it easy to remember. For example, we would normally have given Rupert the addresses 10.1.1.163 and 10.2.2.163. However, here we haven’t done that, to emphasize that the interfaces are completely unrelated and can have completely different IP numbers.