With the NetworkManager service started, you can manage your network connections from the NetworkManager applet icon. With NetworkManager, you can work with wireless and wired Ethernet connections, as well as select to set up a virtual private network (VPN) from those connections.

# ## Connecting to a Wireless Network

To see wireless networks detected by your computer, click on the NetworkManager applet icon in the top panel. Provided that CentOS has a working driver for your wireless card, you will see a list of wireless networks that have been detected.

> Although support for wireless LAN cards has dramatically improved in recent releases, there are still many wireless cards that are not supported out-of-the-box. If your wireless card is not properly detected, refer to the “Getting Wireless Drivers” section later in this chapter for descriptions of how to get and load appropriate wireless drivers.

Assuming that the network you want to connect to shows up under the “Wireless Networks” heading, you can click on that network. Type a password or encryption key and click Connect when you see the Wireless Network Secrets Required window.

If the password is correct, NetworkManager will use your new wireless connection as the default network route from your computer (disconnecting any wired Ethernet connection you may have).

Here are some other ways to work with wireless networks from the NetworkManager applet:

+   1. **Existing Wireless Network** — If your wireless card is working, but the network you want doesn't appear, click on the NetworkManager icon and select “Connect to Other Wireless Network” to select a different wireless network by name.
+   2. **New Wireless Network** — To create your own wireless network, click on the NetworkManager icon and select “Create New Wireless Network.” When prompted, enter the network name and select the type of Wireless Security you want. You can then enter the passphrase that others would use to connect to your new wireless network.
+   3. **Disable Wireless Network** — Right-click on the NetworkManager applet icon and uncheck the “Enable Wireless” box (so the checkbox disappears).

After you have established a connection, you can check information about that connection by right-clicking on the NetworkManager icon and selecting “Connection Information.” You will see the interface name, connection speed, driver name, IP address, and locations of DNS servers (among other information).

# ## Connecting to a Wired Network

As noted earlier, with your wired network plugged in and a DHCP server on the line, you probably don't have to do anything to start your wired Ethernet network interface. However, if you