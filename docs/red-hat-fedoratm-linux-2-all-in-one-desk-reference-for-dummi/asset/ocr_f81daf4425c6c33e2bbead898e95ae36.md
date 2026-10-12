+   ❖ Cat 5 UTP cables to connect the two Ethernet cards to their networks — one goes to the Ethernet hub on the home network and the other to the Internet connection (a DSL or cable modem).
+   
+   ❖ A connection to the Internet, the higher the bandwidth the better.

# ## Steps to follow

Log in as root and follow these steps to set up the Fedora Core system as a NAT router:

+   1. **Enable IP forwarding in the kernel by typing the following command in a terminal window:**
+   
+   ```bash
+    echo "1" > /proc/sys/net/ipv4/ip_forward
+   ```
+   
+   This step is necessary because IP forwarding is disabled by default. To ensure that IP forwarding is enabled when you reboot your system, add this line to the /etc/rc.d/rc.local text file.

+   2. **Type iptables to run the IP packet filter administration program and set up the rules that enable the Fedora Core PC to perform network address translation (NAT) for your home network.**
+   
+   The exact iptables command depends on the network interface through which the Fedora Core system connects to the Internet. For example, if the Internet connection is through the eth0 network interface, use the following command:
+   
+   ```bash
+    iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
+   ```
+   
+   You can also add packet filtering to ensure that no new connections can come in through the eth0 interface. The following two commands turn on this packet filtering:
+   
+   ```bash
+    iptables -A INPUT -i pp0 -m state --state NEW,INVALID -j DROP
+    iptables -A FORWARD -i pp0 -m state --state NEW,INVALID -j DROP
+   ```

+   3. **Save the iptables settings with the following command:**
+   
+   ```bash
+    service iptables save
+   ```
+   
+   This command saves the iptables rules in the /etc/sysconfig/iptables file. From then on, whenever you start the Fedora Core system, iptables automatically loads these rules and sets up the system as a NAT router.