```
    ends 2 2002/05/04 15:48:12;
    hardware ethernet 00:50:ba:d8:03:9e;
    client-hostname "pine";
}

```

+   - Turn on the Ethereal window (from the GNOME menu, choose Programs  $\rightarrow $ Internet  $\rightarrow $ ethereal) and start capturing data (in promiscuous mode). Restart the DHCP server and restart the network interface on the client. You should see a series of DHCP packets that show a sequence that looks like the following: DHCP Offer, DHCP Discover, DHCP Offer, DHCP Request, and DHCP ACK.
+   - From the client computer, you should be able to start communicating on the network. If the client is a Linux system, type the ifconfig -a command. Your Ethernet interface (probably eth0) should appear, with the IP address set to the address assigned by the DHCP server.

When the server is running properly, you can continue to add DHCP clients to your network to draw on the pool of addresses you assign.

# # Setting Up a DHCP Client

Configuring a network client to get addresses from your DHCP server is fairly easy. Different types of operating systems, however, have different ways of using DHCP. Here are examples for setting up Windows and Red Hat Linux DHCP clients.

**Windows:**

+   1. From most Windows operating systems (Windows 95, 98, ME, and so on), you open the Network window from the Control Panel (Start $\rightarrow$ Settings $\rightarrow$ Control Panel).
+   2. From the Configuration tab, click the TCP/IP interface associated with your Ethernet card (something like TCP/IP $\rightarrow$ 3Com EtherLink III).
+   3. Click Properties. The Properties window appears.
+   4. Click the IP Address tab and then select "Obtain an IP Address Automatically".
+   5. Click OK and reboot the computer so the client can pick up the new IP address.

**Red Hat Linux:**

+   1. While you are initially installing Red Hat Linux, click Configure using DHCP on the Network Configuration screen. Your network client should automatically pick up its IP address from your DHCP server when it starts up.
+   2. To set up DHCP after installation, open the Network Configuration window (neat command).
+   3. From the Network Configuration window: