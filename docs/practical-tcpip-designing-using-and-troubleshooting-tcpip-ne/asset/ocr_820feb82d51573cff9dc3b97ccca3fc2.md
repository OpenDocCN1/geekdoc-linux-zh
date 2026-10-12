# ## 27.10 Building a test network for VPN

A technique that saves us a huge amount of time is to “glue on” a test network to our live LAN. Let’s say we’re going to install a VPN firewall at our new office in New York (“NY”). Our aims are to:

+   * install the test firewall alongside the live network in Cambridge (“CAM”), so we can check out VPN, etc.
+   * configure the New York firewall/VPN fully, so it can be slotted into the real remote site without any extra configuration. We’ll just courier it over to the new office, and have someone connect it up. We want to avoid sending an engineer over if possible.

However, there are many constraints:

+   * we’re working on our live network, so CAM’s Internet connectivity must not be disrupted for more than a minute or two at most
+   * the CAM router is managed by the ISP, and we can’t alter it. Therefore we need another way to route traffic between the CAM and NY networks. We’ll insert a temporary extra router to do this
+   * the NY firewall must be outside the live CAM firewall, so VPN and firewall rules for NY/CAM traffic are exercised
+   * the NY firewall must be inside CAM’s ISP’s router. It will have public IP addresses that really belong in NY; if any packets for these appeared on the network outside the CAM live router, they would be routed to NY.

We build the network shown in Figure 27.15 here in Cambridge. We’ve used a Linux box as the extra router; if you use an NT box instead, the steps are the same but the commands to apply the settings will of course be different.

![](bbox=[0.15, 0.59, 0.88, 0.93])