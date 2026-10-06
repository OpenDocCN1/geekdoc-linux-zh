# Chapter 1 \ Installing SUSE 31

![](bbox=[0.181, 0.125, 0.818, 0.506])

Figure-1-22: Configuring network cards

For most people using SUSE in a business environment, a DHCP server may already be running, and address domain name system (DNS) server list, and router configuration will be available. Home users and users setting up a server will find it necessary to configure these details manually. Home users with simple broadband or dial-up connections often automatically receive this infor mion from their Internet service providers (ISPs) and may not need to change these settings.

To change the configuration of the network card, "Network Interfaces" and select the network card in question (if you have multiple network cards), and click the Edit button. A similar to the one shown in Figure 1-23 appears.

In this example, we set the IP address of the network card to 192.168.0.1/255.255.255.0, with a router/gateway of 192.168.0.8 and a DNS server of 192.168.0.254. If you are unfamiliar with these terms at this stage, see Chapter 6 for additional information.

To change the configuration of the network card from automatic to manual, select Static address setup. This enables you to edit the IP and subnet mask fields. As you can see in Figure 1-23, we have set the IP address/netmask to that of the configura-tion we talked about in the preceding paragraph.