# Chapter 23: Setting Up a DHCP Boot Server

+   - Launch Wireshark (yum install wireshark to install and wireshark& to run) and start capturing data (in promiscuous mode). Restart server and restart the network interface on the client. You should see a series of DHCP packets that show a sequence like the following: DHCP Discover, DHCP Offer, DHCP Request, and DHCP ACK.

+   - From the client computer, you should be able to start communicating on the network. If the client is a Linux system, use ifconfig -a command. Your Ethernet interface (probably eth0) should appear, with the IP address assigned by the DHCP server. If your client is a Windows system, open a command prompt and type ifconfig /all. You will see the configuration information for all of your network interfaces.

When the server is running properly, you can continue to add DHCP clients to your network and draw on the pool of addresses you choose.

# Setting Up a DHCP Client

Most client computers (Window, Linux, or Mac) are configured by default to boot up using DCHP to connect to the network. However, when that is not the case, you may need to manually indicate that DCHP be used.

Configuring a network client to get addresses from your DHCP server is fairly easy. Different types of operating systems, have different ways of using DHCP. Here are examples for setting up Windows and Linux DHCP clients.

# Windows (Vista)

+   1. From Windows Vista, select Start -> Control Panel -> Network and Internet -> Network and Sharing Center -> Manage Network Connections.

+   2. Select Local Area Connection.

+   3. Select Properties. The Properties window appears.

+   4. Select Internet Protocol Version 4 and click Properties.

+   5. On the General tab, make sure the Obtain an IP Address Automatically button is selected.

# Windows (95, 98, 2000, or XP)

+   1. From most older operating systems (Windows 95, 98, and 2000), you open the Network window from the Control Panel (Start -> Settings -> Control Panel). For Windows XP systems, select Start -> Control Panel -> Network and Internet Connections -> Network Connections, and then select your Local Area Connection and choose Properties.

+   2. From the Configuration tab (or General tab in Windows XP), click the TCP/IP interface associated with your Ethernet card (something like TCP/IP -> 3Com EtherLink III).