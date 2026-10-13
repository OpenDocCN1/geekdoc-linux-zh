# # TROUBLESHOOTING

*I have a PCI card that has the tulip chip on it. When I modprobe tulip, the link light comes on, but when I start the network, the link light goes out and I can’t talk to the network.*

Looks like you’ve run into the tulip versus old_tulip problem. Try the old_tulip first. If that doesn’t work it might use the even older de4x5 module. The same is true for other chipsets, such as some of the RealTech chipsets. Some use the rt18129 module, but others will use the ne2000 (ne) or ne2k-pci module. You might have to experiment or check with the NIC manufacturer.

*I set up a network and HostX can ping HostA (the Internet gateway), but can’t seem to reach the Internet even though HostA can.*

Perform the following steps:

+   1. Ensure HostX has HostA listed as its default route by issuing the command `netstat -rn` on HostX. The last line of output should look like the following:
+   
+      ```text
+      0.0.0.0          192.168.0.1     0.0.0.0        UG       40 0          0 eth0
+      ```
+   
+      You should have only one `0.0.0.0` line containing UG in the flags section.
+   
+   2. On your gateway system (HostA), make sure you have a similar line to the one above that points to the remote system connected to your Internet connection.
+   
+   3. Ensure forwarding is turned on in your gateway system (HostA) by issuing the command `cat /proc/sys/net/ipv4/ip_forward`. You should get a 1 as an answer.
+   
+   4. Ensure you have a rule permitting IP masquerading if necessary as shown above (check with iptables -l). Your specific ruleset will be determined by whether you have a dynamically assigned IP (MASQUERADE) or a statically assigned IP (SNAT). For more information, see Chapter 35, “IP Masquerading.”
+   
+   5. If you still can’t connect from HostX, ensure you can resolve domain names using nslookup or dig. If you can’t, check your `/etc/resolv.conf` file and make sure you have at least two valid nameserver lines and the IPs listed are good.

*I can’t connect to any Internet site by name, but I seem to be able to connect by IP address. What’s wrong?*

Step 5 in the previous question covers the answer. You don’t have valid nameserver listed in your `/etc/resolv.conf` file. Check with your ISP for valid IPs and put them in this file using coostool.

*I bought some Ethernet cards, a hub, and some cables. The Ethernet cards look like they should be working—that is, I see blinking link lights on the Ethernet cards, but the hub link lights don’t light.*

You can have mixed and matched 10MB cards or hubs with 100MB cards/hubs. All system components need to be able to talk at the same speed, so if you have 10MB cards and a 100MB hub, you won’t be able to communicate. Also make sure, if you’re using 100MB or faster components, that you’ve purchased a good category 5 straight-through cable and not