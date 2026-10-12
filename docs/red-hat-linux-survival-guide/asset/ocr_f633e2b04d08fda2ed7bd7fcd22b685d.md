on using this computer as a co-located Web server on an ISP network, you can turn IP forwarding off by setting this option to no.

The next two lines specify the host name of the computer and the domain name of your network. The host name you specify here must include the domain name you specify in the DOMAINNAME line. In other words, don't specify a host name that uses a different domain name from the name you state in the DOMAINNAME line.

The next two lines specify the information that you need to determine the default gateway for a computer. A default gateway is a computer (or a router) that transfers packets to and from your computer. For example, if you intend to connect your Red Hat Linux computer to your LAN, where you have an ISDN router that connects the LAN to the Internet, specify the IP address of the ISDN router's network interface as the default gateway.

GATEWAYDEV is important when you have multiple network interfaces. If you have only one Ethernet device, you should always set this to eth0. If you have multiple Ethernet devices (eth0, eth1, and so on), you have to use the interface name connected to the default gateway.

After you configure the /etc/sysconfig/network file, you are ready to create the network interface file in the /etc/sysconfig/network-scripts directory. The network interface file uses ifcfg-interface as the naming convention. For example, the network interface filename for eth0 is ifcfg-eth0. An example of this file is shown in Listing 6-2.

# Listing 6-2 An example /etc/sysconfig/network-scripts/ifcfg-eth0 file

```
DEVICE=eth0
IPADDR=206.171.50.50
NETMASK=255.255.255.240
NETWORK=206.171.50.48
BROADCAST=206.171.50.63
ONBOOT=yes
BOOTPROTO=static
```

Before you can configure the information in this file, you have to obtain the network address, the network mask, the IP address for the network interface on the host, and the broadcast address from your Internet service provider. (I discuss the network mask and broadcast address further in a later section.)

The first line in this file specifies the device name. The second line specifies the network mask (netmask) number. The third line specifies the