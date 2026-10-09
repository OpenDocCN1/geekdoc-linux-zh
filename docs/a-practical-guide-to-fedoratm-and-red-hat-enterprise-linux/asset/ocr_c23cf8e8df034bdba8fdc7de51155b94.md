# DHCP CLIENT

A DHCP client requests network configuration parameters from the DHCP server and uses those parameters to configure its network interface.

# PREREQUISITES

Make sure the following package is installed:

+   • dhclient

# dhclient: THE DHCP CLIENT

When a DHCP client system connects to the network, dhclient requests a lease from the DHCP server and configures the client's network interface(s). Once a DHCP client has requested and established a lease, it stores the lease information in a file named dhclient-*-interface.lease, which resides in the /var/lib/NetworkManager directory. The interface is the name of the interface the client uses, such as eth0. The system uses this information to reestablish a lease when either the server or the client needs to reboot. The DHCP client configuration file, /etc/dhcp/dhclient.conf, is required only for custom configurations. The /usr/share/doc/dhclient* directory holds a well-commented dhclient.conf file.

The following dhclient.conf file specifies a single interface, ens33:

```
$ cat /etc/dhcp/dhclient.conf
interface "ens33" {
 send dhcp-client-identifier 1:xx:xx:xx:xx:xx:xx:xx;
 send dhcp-lease-time 86400;
}
```

In the preceding file, the 1 in the dhcp-client-identifier specifies an Ethernet network and xx:xx:xx:xx:xx:xx is the MAC address (page 1259) of the device controlling that interface. See page 494 for instructions on how to determine the MAC address of a device. The dhcp-lease-time is the duration, in seconds, of the lease on the IP address. While the client is connected to the network, dhclient automatically renews the lease each time half of the lease time is up. A lease time of 86,400 seconds (one day) is a reasonable choice for a workstation.

# DHCP SERVER

A DHCP server maintains a list of IP addresses and other configuration parameters. Clients request network configuration parameters from the server. The DHCP server does not ship with a working configuration. See the /usr/share/doc/dhcp/*/example files for sample dhcpd.conf files that include a lot of documentation.

# PREREQUISITES

Install the following package:

+   • dhcp