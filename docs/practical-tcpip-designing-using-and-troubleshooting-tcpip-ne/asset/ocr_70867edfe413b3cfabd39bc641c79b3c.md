# ### 23.7 IP addressing for the live network

In the previous module we explained how to handle public/private addressing for the preliminary testing of your Internet connection. In this module we assume your connection has been tested and is working OK. You now have to insert your firewall into your network and configure your IP addressing for live running.

# **1. At least one public, static IP address**

There are two variants here:

+   * i. many public, static IP addresses. You may choose to use NAT or not. If you do, the NATing will be performed by your firewall. (Typical examples: ADSL for business use, permanent leased line.)

+   * ii. a single, public, static IP address. If you want more than one machine on your LAN (and we assume you will), you must use NAT, performed by your firewall; otherwise, this is just a small instance of (i) above. (Typical examples: analog dial-up or ADSL for home use.)

![](bbox=[0.12, 0.4, 0.6, 0.63])

![](bbox=[0.62, 0.4, 0.93, 0.63])

**Figure 23.8** Allocating IP addresses to machines on your live LAN

All the machines use the static, public addresses during testing (1a, Figure 23.7). If you're not going to use NAT, adding the firewall (1b, Figure 23.8) is very easy because you continue to use the numbers from testing. If you do implement NAT, it becomes active only after you add your firewall, so you will have to renumber your test machines after the firewall is installed (1c, Figure 23.8). However, as we install only one or two machines for testing, this is a very small job.

If you have only one address, you will have to omit step K (Module 23.9 – adding extra machines) from your testing until you add a firewall (1c Figure 23.8). For reasons of space we won't treat this as a special case any more – it's just an instance of case (ii) with NAT.

If you chose (probably unwisely) not to implement a firewall, then your test configuration (1a or 2a) will be your final, live configuration too.