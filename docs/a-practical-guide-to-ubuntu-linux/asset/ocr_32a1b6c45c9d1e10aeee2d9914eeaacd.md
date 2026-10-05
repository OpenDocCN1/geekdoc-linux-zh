# CHAPTER 11 SYSTEM ADMINISTRATION: CORE CONCEPTS

The preceding configuration file assigns addresses in the range 192.168.1.2 to 192.168.1.200. The DHCP server starts at the bottom of this range and attempts to assign a new IP address to each new client. Once the DHCP server reaches the top of the range, it starts reassignment IP addresses that have been used in the past but are not currently in use. If you have fewer systems than IP addresses, the IP address of each system should remain constant. Two systems cannot use the same IP address at the same time.

Once you have configured a DHCP server, restart using the dhcpd init script (page 473). When the server is running, clients configured from the server using DHCP should be able to obtain an IP address to do so.

# STATIC IP ADDRESSES

As mentioned earlier, routers and servers typically require static IP addresses. Although you can manually configure IP addresses for these systems, it may be more convenient to use the DHCP server provide them with static IP addresses.
When a system that requires a static IP address connects to the network and contacts the DHCP server, the server needs to identify the system so it can assign the proper IP address to that system. The DHCP server uses the MAC address (page 1158) of the system's Ethernet card (NIC) as an identifier. When you set up the server, you must know the MAC address of each system that requires a static IP address.

Determining the MAC The ifconfig utility displays the MAC addresses of the Ethernet cards in a system. Following the example, the MAC addresses are the colon-separated of hexadecimal numbers following Hwaddr:

```
$ ifconfig | grep -i hwaddr
eth0 Link enc:Ethernet Hwaddr BA:00:DF:C0:FF
eth1 Link enc:Ethernet Hwaddr 00:02:B3:41:35:98
```

Run ifconfig on each system that requires a static IP address. Once you have determined the MAC addresses of these systems, you can add a host section to the /etc/dhcp3/dhcpd.conf file for each one, instructing the DHCP server to assign a specific address to that system. The following host section assigns the address 192.168.1.1 to the system with the MAC address of BA:00:DF:C0:FF:

```
$ cat /etc/dhcp3/dhcpd.conf
host router {
  hardware BA:00:DF:C0:FF;
  fixed-address 192.168.1.1;
  option host-name router;
}
```

The name following host is used internally by dhcpd. The name specified after option host-name is passed to the client and can be a hostname or FQDN. After making changes to dhcpd.conf, restart dhcpd using the dhcpd init script (page 473).