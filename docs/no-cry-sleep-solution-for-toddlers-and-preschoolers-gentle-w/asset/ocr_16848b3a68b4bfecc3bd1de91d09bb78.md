The current version of DHCP now supports the DHCP failover protocol in which two DHCP servers support the same address pool. Should one fail, the other can continue to provide DHCP services for a network. Primary and secondary servers in this scheme are designated with the primary and secondary statements.

A variety of DHCP servers and clients are available for different operating systems. For Linux, you can obtain DHCP software from the Internet Software Consortium (ISC) at www.isc.org. The software package includes a DHCP server, a client, and a relay agent. Linux includes a DHCP server and client. The DHCP client is called dhcpc, and the server is called dhcpd. The network information a DHCP client downloads is kept in its own network configuration files in the /etc/dhcpcd directory. For example, here you can find a resolv.conf file for your network’s name servers.

# Configuring DHCP Client Hosts

Configuring hosts to use a DHCP server is a simple matter of setting options for the host’s network interface device, such as an Ethernet card. For a Linux host, you can use a distribution network tool to set the host to automatically access a DHCP server for network information. On a network tool’s panel for configuring the Internet connection, you will normally find a check box for selecting DHCP. Clicking this box will enable DHCP. For Red Hat, you can use the redhat-config-network tool and select the network device on the Devices panel and edit it. On the General panel, click the entry labeled Automatically Obtain IP Address Settings With, and be sure DHCP is selected from the pop-up menu. If you are connecting to an Internet service provider (ISP), under the DHCP Setting, click Automatically Obtain DNS Information From Provider. On Red Hat, the BOOTPROTO entry to DHCP will be set in that interface’s network script in the /etc/sysconfig/network-scripts directory, such as ifcfg-eth0 for the first Ethernet card. You could also manually make this entry:

```
BOOTPROTO=dhcp
```

Be sure to restart your network devices with the network script to have the changes take effect. The information that is being provided to a client by a DHCP server is listed in the client’s /etc/dhcpcd directory. Here you will find information files for the client’s specific network device. For example, information provided for the first Ethernet device will be listed in the /etc/dhcpcd/dhcpcd-eth0.info file. You will find information such as the IP address, netmask, broadcast address, the hostname, domain name, and the DNS servers—all assigned by the DHCP server to the client.

On a Windows client, locate the TCP/IP entry for your network interface card, then open its properties window. Click the box labeled Obtain IP Address Automatically. Then locate the Wins panel (usually by clicking the Advanced button) and select DHCP as the protocol you want to use.

# Configuring the DHCP Server

On Red Hat systems, you can stop and start the DHCP server using the dhcpd command in the /etc/rc.d/init.d directory. Use the redhat-config-services tool or the service command with the start, restart, and stop options. The following example starts the DHCP server. Use the stop option to shut it down, and restart will restart it.

```
service dhcpd start
```