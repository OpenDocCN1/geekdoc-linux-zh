
The next dialog is independent of the method you choose. It lists the detected network cards. See Figure 5-2.

![](img/9129877170834ca9d5fdac5319bf5f12_122_0.png)

Figure 5-2

Usually the cards are autodetected by YaST, and the correct kernel module is used. Select the card you want to configure; then select Edit. The dialog that appears is shown in Figure 5-4.

If the card is not recognized by YaST, the required module must be entered manually. Select Add. A Manual Network Card Configuration dialog appears. See Figure 5-3.

From this dialog, you can configure the following:

- *Network Configuration*—Specify the network Device Type (Ethernet, Bluetooth, Wireless, etc.) and the Configuration Name (0, 1, etc.).
- *Kernel Module*—If your network card is a PCMCIA or USB device, select the corresponding check boxes and confirm by selecting Next. Otherwise, select Select from List and select your network card from the list. YaST automatically adds the appropriate driver for the selected card to the Module Name drop-down list, as well as any options to the Options text box. Confirm by selecting OK.

![](img/9129877170834ca9d5fdac5319bf5f12_123_0.png)

Figure 5-3

After selecting Next, the dialog shown in Figure 5-4 appears.

It is the same dialog you see when selecting an existing network card entry in the YaST Network Card Configuration Overview and selecting Edit.

The Address tab offers the following configuration options:

- *None Address Setup*—Select this if you do not want an IP address for this interface.
- *Automatic Address Setup (via DHCP)*—If your network has a DHCP server, you can set up your network address automatically. You should also use this option if you are using a DSL line with no static IP address assigned by the ISP.

If you decide to use DHCP, you can configure the details after selecting DHCP Options from the Advanced drop-down list. Specify whether the DHCP server should always broadcast its responses (in this case, select Request Broadcast Response) and any identifier to use.

By default, DHCP servers use the network card’s hardware address to identify an interface. If you have a virtual host setup where different hosts communicate through the same interface, an identifier is necessary to distinguish them.

![](img/9129877170834ca9d5fdac5319bf5f12_124_0.png)

Figure 5-4

- *Static Address Setup*—If you have a static address, select the corresponding check box.
- *IP Address*—Each computer accessible in the network has at least one address for each network interface, which must be unique in the entire network. According to the currently valid standard (IPv4), this address consists of a sequence of four bytes, separated by dots (such as 10.10.0.69).

When choosing the IP address, you need to know if the computer will be directly connected to the Internet. In this case, use an assigned official IP address. Otherwise, use an address from the private address space used in the network.

- *Subnet Mask*—The network mask (referred to as subnet mask in YaST), determines in which network an IP address is located.

The mask divides the IP address into a network section and a host section, thus defining the size of a network. All computers within the network can reach each other directly without a router.

- *Hostname and Name Server*—Computers in the network can be addressed directly using their IP addresses or with a unique name. A name server (Domain Name System DNS) must exist for the resolution of names into IP addresses and vice versa.

After selecting **Hostname and Name Server** and if you are using DHCP, the dialog shown in Figure 5-5 appears.

![](img/9129877170834ca9d5fdac5319bf5f12_125_0.png)

Figure 5-5

If you want to change data delivered by DHCP (for example, the IP number), select **Modify**. If you only want to change other information, you can select **Accept** here. The dialog shown in Figure 5-6 appears.

![](img/9129877170834ca9d5fdac5319bf5f12_125_1.png)

Figure 5-6

This dialog lets you enter the following:

- *Hostname*—Enter a name by which the computer can be addressed. This name should be unique within the network.
- *Domain Name*—This is the name of the DNS domain to which the computer belongs. Domains help to divide networks. All computers in a defined organizational area normally belong to the same domain.

A computer can be addressed uniquely by giving its FQDN (Fully Qualified Domain Name). This consists of the hostname and the name of the domain, such as `da10.digitalairlines.com`. In this case, the domain would be `digitalairlines.com`.
- *List of name servers*—To address other computers in the network with their hostnames, identify the name servers that will be responsible for converting computer names to IP addresses and vice versa.

You can specify a maximum of three name servers.
- *Domain search list*—In the local network, it is more convenient to address other hosts with their hostnames rather than their FQDNs. The domain search list specifies the domains with which the system can expand the hostname to the FQDN.

This complete name is then passed to the name server to be resolved. For example, `da10` is expanded with the search list `digitalairlines.com` to the FQDN `da10.digitalairlines.com`. This name is then passed to the name server to be resolved.

If the search list contains several domains, one after the other is used, and the resulting FQDN is passed to the name server until an entry returns an associated IP address.

Separate the domains with commas or white space.
- *Routing*—If the computer is intended only to reach other computers in the same subnet, then it is not necessary to enter any routes.

However, if you need to enter a default gateway or create a routing table, select **Routing** from the Network Address Setup dialog. The window shown in Figure 5-7 appears.

You can define the following:

- *Default Gateway*—If the network has a gateway (a computer that forwards information from a network to other networks), its address can be specified in the network configuration.

All data not addressed to the local network is then forwarded directly to the gateway.
- *Routing Table*—You can create entries in the routing table of the system after selecting Expert Configuration.
- *Enable IP Forwarding*—If you have two network cards in your computer and you select this option, IP packets that are not addressed to your computer are routed from one network interface to the other as needed.

![](img/9129877170834ca9d5fdac5319bf5f12_126_0.png)

![](img/9129877170834ca9d5fdac5319bf5f12_127_0.png)

Figure 5-7

- *Advanced*—Configure Hardware Details, DHCP Options, Additional Addresses, or IPv6. All the necessary information is now available to activate the network card. On the General tab of the Network Address Setup dialog, you can define a few more options. See Figure 5-8.
- *Firewall Zone*—You can specify the zone to which the interface belongs. The following zones are possible:
  - No Zone, All Traffic Blocked
  - Internal Zone (Unprotected)
  - Demilitarized Zone
  - External Zone

![](img/9129877170834ca9d5fdac5319bf5f12_128_0.png)

Figure 5-8

- **Device Activation**—Choose when the interface should be set up. Possible values are:
  - *At Boot Time*—During system start.
  - *On Cable Connection*—If there is a physical network connection.
  - *On Hotplug*—When the hardware is plugged in.
  - *Manually*
  - *Never*
  - *On NFSroot*—When you have an NFS or iSCSI root file system.

Normally only root is allowed to activate and deactivate a network interface. To allow this for normal users, activate the option **User Controlled**. The values are explained in the help text on the left side of the dialog.
- **MTU (Maximum Transfer Unit)**—Maximum size of an IP package. The size depends on the hardware (Ethernet: max. 1500 bytes).

Select **Next** to close the Network Address Setup dialog.
