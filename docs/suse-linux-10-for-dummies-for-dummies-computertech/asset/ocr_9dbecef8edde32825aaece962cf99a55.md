![](bbox=[0.133, 0.124, 0.208, 0.196])

The Linux kernel loads the driver for the Ethernet card every time it boots.
To verify that the Ethernet driver is loaded, type the following command in a
terminal window:

```
dmesg | grep eth0
```

On one of my PCs, I get the following output when I type that command:

```
eth0: RealTek RTL8139 at 0xf0d16000, 00:0c:76:f4:38:b3, IRQ 161
eth0: Identified 8139 chip type 'RTL-8101'
eth0: link up, 100Mbps, full-duplex, lpa 0x45E1
eth0: no IPv6 routers present
```

You should see something similar, showing the name of your Ethernet card
and other related information.

# Configuring the Ethernet Network

When you set up the network during SUSE Linux installation, the installation
program prepares all appropriate configuration files using the information
you provide. You therefore typically never have to manually configure the
network. However, SUSE Linux comes with GUI tools to configure the network
devices, just in case something needs changing.

To configure the Ethernet network interface, follow these steps:

+   1. **Choose Main Menu→System→YaST from the KDE desktop (choose Desktop Menu→YaST from the GNOME desktop).**
+   
+      This opens the YaST Control Center.
+   
+   2. **Select Network Devices on the left-hand pane of the YaST Control Center window and Network Card on the right-hand pane.**
+   
+      YaST then brings up a window (shown in Figure 8-2) with information about the already configured network card and any new network cards that it detects.
+   
+   3. **Select your network card (assuming it’s not yet configured) and click Configure. To change an already configured card, click Change.**
+   
+      Provide the requested information such as how the IP address is obtained (typically, the answer is DHCP or dynamic).