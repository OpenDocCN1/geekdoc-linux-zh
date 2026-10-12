# ### 2.12 Lab – building the simplest network possible: implement and test

![](bbox=[0.2, 0.15, 0.82, 0.27])

**Figure 2.22** IP addresses and netmasks for simple test network

Figure 2.22 shows the network we want to build, with the IP addresses we’ll allocate. We’re going to configure it and then experiment with it: we’ll change settings one by one, to force errors and observe the system’s behavior.

If you are already running **tcpdump** on A or B, you can omit the separate **tcpdump** machine. If you include a sniffer machine in the network, it doesn’t need any particular IP address because it’s only sniffing the network in promiscuous mode and doesn’t have to send anything or receive anything in the normal way. As long as its TCP/IP is up and running, it will work. However, if you set its parameters as shown, you can use it as another host on the LAN to perform tests from, which will be useful.

As we mentioned in Module 2.2, the three crucial networking parameters are IP address, netmask, and default gateway. (The default gateway is concerned with routing to other networks. We have only a single network here, so we don’t need the default gateway at all in this chapter; we defer explaining it until the next chapter.)

+   * we have chosen IP addresses in the 10.x.x.x range because they are specially reserved for use on private networks and are not allocated to any specific site (Module 4.9). We’ve chosen the series 10.9.8.x as it’s easy to remember
+   * don’t use addresses 10.9.8.0 or 10.9.8.255 – they are special (Module 4.10) and using them may cause you problems
+   * we have chosen netmask 255.255.255.0, giving a range consisting of the 256 IP addresses that have the same first three bytes as the machine’s IP address:

| A | 10.9.8.1 | 10.9.8.0–10.9.8.255 |
| B | 10.9.8.2 | 10.9.8.0–10.9.8.255 |

| IP address | Range derived from IP address combined with 255.255.255.0 netmask |

+   * which is what we want – both machines have the same view of the world
+   * we have shown the PCs in the diagram without any names but marked as A and B to make it easy to refer to them in the text. You don’t have to set the machine name, but if it is set, it doesn’t matter.