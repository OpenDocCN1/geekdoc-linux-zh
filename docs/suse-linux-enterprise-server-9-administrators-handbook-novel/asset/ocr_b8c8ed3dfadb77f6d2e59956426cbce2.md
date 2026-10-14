# Specifying Network Settings

The next step is to configure your network connectivity. YaST will probe for and auto-detect network cards, modems, ISDN cards, and DSL devices (see Figure 1.10). In most cases, unless you use DHCP to assign a server's network information, the network card configuration would need to be modified.

**FIGURE 1.10**

Network Configuration screen.

![](bbox=[0.156, 0.289, 0.912, 0.642])

Click Change and select Network Interfaces. Next, select the card you want to modify and click its Change button. Finally, highlight the network card and click Edit. By default, YaST sets up the network card for DHCP, but you may want to use statically assigned values instead:

+   - To use a static IP address, change the setup method and enter the server's IP address and netmask (see Figure 1.11).
+   - When not using DHCP, you need to configure a hostname and DNS server information for the server. Click Host Name and Name Server to make the changes; the default hostname is linux and its default domain name is site.
+   - Click Routing and enter the IP address of your nearest router in the Default Gateway field.