# Configuring the ISDN Network Interface via YaST

After you're finished configuring the hardware part, you must configure the network layer for the ISDN interface. YaST makes it easy for you. You only have to decide which protocol you will be using. This depends on your ISP. The following are the three main ISDN protocols:

+   - syncPPP
+   - rawIP·HDLC
+   - Terminal login (x. 75)

The steps to set up the first two protocols are almost the same. Only the last part differs.

# The ISDN syncPPP Protocol

Follow these steps to set up the syncPPP protocol:

+   1. Launch YaST as root.
+   2. From the menu, choose System Administration, Network Configuration, Network Base Configuration. The Selection of Network dialog appears (see Figure 23.15).

FIGURE 23.15
ISDN network configuration via YaST.

![](bbox=[0.28, 0.55, 0.75, 0.82])

+   3. Choose an empty number and press F5. This will enable you to select the proper device for the network interface.
+   4. Select the ISDN syncPPP protocol. This is one of the protocols to be used when using ISDN connections.
+   5. Enter your IP and your PtP IP (partner's IP). If you don't know these IPs or you use a dynamic IP with syncIP, use any values (192.168.0.100 and 192.168.0.101 will work just fine).
+   6. After you test your connection, issue the ifconfig command and get your ISP's IP through its output.