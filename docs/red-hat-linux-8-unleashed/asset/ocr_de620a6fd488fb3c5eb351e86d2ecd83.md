# CHAPTER 13 Network Connectivity

![](bbox=[0.207, 0.073, 0.822, 0.442])

FIGURE 13.3 Configure an Ethernet device in the Devices tab of the Network Configuration tool screen.

# # Dynamic Host Configuration Protocol

As the name implies, Dynamic Host Configuration Protocol (DHCP) configures hosts for connection to your network. DHCP allows a network administrator to configure all TCP/IP parameters for each host as it connects to the network after activation of a NIC. These parameters include automatically assigning an IP address to a NIC, setting name server entries in /etc/resolv.conf, and configuring default route and gateway information for a host. This section describes how to set up a DHCP server using Red Hat Linux.

> > NOTE You can learn more about DHCP by reading RFC2131 “Dynamic Host Corfiguration Protocol.\”

# ## How DHCP Works

DHCP provides persistent storage of network parameters by holding identifying information for each network client that might connect to the network. The three most common pairs of identifying information are

+   * Subnet/host address—Used by hosts to connect to the network at will
* Subnet/hostname—Enables the specified host to connect to the subnet
* Subnet/hardware address—Enables a specific client to connect to the network after getting the hostname from DHCP