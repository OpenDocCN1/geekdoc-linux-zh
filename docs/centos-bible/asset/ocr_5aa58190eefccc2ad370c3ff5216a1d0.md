# **FIGURE 13-2**

Using iptables as a firewall between the Internet and a LAN

![](bbox=[0.12, 0.165, 0.875, 0.405])

# **Firewall Computer**

The firewall computer is set up as follows:

+   * **Local Host**—127.0.0.1 (IP address) and lo (interface). You shouldn't need to change these.
+   * **Connection to the Internet**—123.45.67.89 (IP address) and eth0 (interface). Replace them with the static IP address and interface name associated with your connection to the Internet, respectively.
+   * **Connection to the LAN**—10.0.0.1 (IP address) and eth1 (interface). Replace 10.0.0.1 and eth1 with the static IP address and interface name associated with your connection to your LAN, respectively.
+   * **Computers on the LAN**—Each computer on the LAN in the example has an IP address from 10.0.0.2 to 10.0.0.254. Change 10.0.0.255 to a number that matches your LAN's range of addresses.

Here is an example of a script to load firewall rules that could be used for the configuration shown in Figure 13-2:

```
# (1) Policies (default)
iptables -P INPUT DROP
iptables -P OUTPUT DROP
iptables -P FORWARD DROP

# (2) User-defined chain for ACCEPTed TCP packets
iptables -N okay
```