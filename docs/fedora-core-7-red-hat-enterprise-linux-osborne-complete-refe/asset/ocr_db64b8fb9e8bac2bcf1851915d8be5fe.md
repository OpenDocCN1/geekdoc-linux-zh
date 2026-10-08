• **Transmit Rate** Usually set to Auto to adjust automatically to degraded transmissions. But you can set a specific rate such as 11M or 1M from the pop-up menu.

• **Key** This is the encryption key for your wireless network. It must be the same for each cell on your network.

On the Configure Network Settings panel, you specify your IP address, whether it is obtained automatically with DHCP or one you enter yourself. For most company wireless networks, the IP address will be obtained automatically. Normally, the DNS servers are also provided. You can, if you wish, also specify a host name.

If you are setting up a local or home network, you will most likely use static IP addresses you select yourself from the private IP pool, beginning with 192.168, such as 192.168.0.1. The static subnet mask for a small local network is usually 255.255.255.0. The Gateway is the IP address for the computer on your network that connects to the Internet, or to a larger network.

You can later edit a wireless connection, making changes. Wireless configuration has the same General and Hardware Device panels as an Ethernet or DSL connection, but instead of a Route panel, it has a Wireless Settings panel, where you can set your mode and network name along with channel, transmit, and key information.

Your configuration setting will be saved in an Ethernet configuration file in the /etc/sysconfig/network-scripts directory. For example, if your wireless card is designated eth1, then its configuration information is saved in the ifcfg-eth1 file. Here you will find the standard Ethernet connection parameters such as the IP address and gateway, as well as wireless parameters such as the channel used, the mode specified, and the encryption key. The standard setting can be modified using system-config-network on that device. You could also modify this file directly to enter additional parameters, like the frequency (FREQ) or sensitivity level (SENS). You can also specify any of the iwconfig parameters using the IWCONFIG option. Enter IWCONFIG followed by an assignment of an option with a value. For example, the following option sets the fragment threshold for packets:

```
IWCONFIG="frag 512"
```

# Virtual Private Networks

A virtual private network lets you create your own private logical network on top of physical network connections, such as the Internet. Using encryption, your private network transmissions are kept secure from the physical network. Though a virtual private network (VPN) has no physical connections of its own and is not a actual network, the secure transmissions it sends have the effect of operating as if the network did exist as separate entities. VPNs make use of tunneling, in which secure transmissions are sent directly through interconnecting systems on a large network like the Internet without being intercepted or, at any point, translated. To implement a VPN, each node has to use the same encryption support software. On Fedora you can choose to use either the newer IPsec tools or the older third-party Crypto IP Encapsulation (CIPE) tool. To use IPsec to set up a VPN, you click the IPsec panel in system-config-network and create a new connection.

# Interface Configuration Scripts: /etc/sysconfig/network-scripts

A network configuration implemented by system-config-network is saved in interface configuration scripts located in the /etc/sysconfig/network-scripts directory. You can edit these scripts directly, changing specific parameters, as discussed previously for