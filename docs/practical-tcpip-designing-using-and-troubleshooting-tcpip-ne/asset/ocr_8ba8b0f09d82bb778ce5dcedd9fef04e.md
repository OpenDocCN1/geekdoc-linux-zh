+   1.  **Configure the extra router:**
+       *   ensure IP forwarding is enabled:
+   
+   ```bash
+   echo 1 > /proc/sys/net/ipv4/ip_forward
+   ```
+   
+       *   set its IP address to an unallocated one from the set of CAM public addresses. Its netmask should match the CAM firewall's external interface.
+   
+   ```bash
+   ifconfig eth0 192.0.0.2.2 netmask 255.255.255.0
+   ```
+   
+       *   create a new interface **eth0:1** to match the real Internet router in NY:
+   
+   ```bash
+   ifconfig eth0:1 1.1.1.57 netmask 255.255.248 up
+   ```
+   
+       By choosing the IP address to match the real NY router, once we've configured the NY firewall, it can be installed in NY without any changes.

This is the crucial step: creating the interface automatically creates a routing table entry for the 1.1.1.57/29 network, so packets from CAM to NY will be sent to the NY firewall, which is exactly what we want

+   *   set the default gateway to be the CAM live router (192.0.2.1) so that traffic for exterior sites can still get out
+   *   connect the extra router into the network as shown. (It will have no effect until other components are changed.)

+   2.  **Configure the NY firewall:**
+       *   private (LAN) IP address = 10.7.7.58, netmask = 255.255.255.0 (or whatever IP address range you want to use in NY)
+       *   public (WAN) IP address = 1.1.1.58 and netmask = 255.255.255.248 (or whatever your NY ISP has allocated)
+       *   default gateway = extra router (1.1.1.57), so that packets can be routed between the NY and CAM networks.

+   3.  **Configure a small NY test LAN**
+       Set up a machine on the test LAN, so we can **ping**, etc. and check out some of the rules, and ensure we have VPN connectivity, etc: IP address = 10.7.7.39, netmask = 255.255.255.0, default gateway = 10.7.7.58.

+   4.  **configure the live, CAM network use the extra router**
+       Only when we do this is anything (apart from the test net) affected.
+       *   we set the default gateway on the CAM firewall = extra router (192.0.2.2) instead of the CAM router. This allows traffic from the CAM network to route to the NY network.

Important: this works only because we're using NAT on the CAM LAN – all the LAN PCs use the *inside* interface of the CAM firewall as their default gateway. If you're not using NAT, their default gateway is almost certainly the live CAM firewall (192.0.2.1) and changing just the firewall's default gateway won't do what you need. You *could* change all the LAN PCs' default gateways manually, but you can do 99% of what you need by setting up a test PC on the CAM LAN, and set its default gateway explicitly = extra router (192.0.2.2). Then you can test connectivity and VPN between it and the NY LAN.

To remove the test network when you're finished, change the default gateway on the CAM firewall back to be the CAM live router (192.0.2.21) and physically disconnect the extra router, test network, etc.