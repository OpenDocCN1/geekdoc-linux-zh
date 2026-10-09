
BOOTP is an older protocol used to dynamically assign network information to clients. The biggest difference between BOOTP and DHCP is that BOOTP is not designed to provide dynamic addresses; instead, it has a table for each device that requests configuration information.

## DHCP Server

The DHCP server component provides configuration information for DHCP clients. The DHCP server provides an IP address, subnet mask, gateway, and other information on request. Configuration of the server can be managed through the command line or through a GUI tool.

DHCP configuration is not standard between Linux distributions. Typically, the server uses two configuration files—/etc/dhcp/dhcpd.conf and /var/lib/dhcp/dhcpd.leases. The dhcpd.conf file contains information for DHCP clients. This includes a range of addresses, gateway, and other information. The dhcpd.leases file also contains configuration information distributed to clients. This includes the IP address and the lease time (how long the IP address is assigned to a specific client).

There are two types of entries in the DHCP configuration file—parameters and declarations. Parameter entries contain network configuration options for clients. Declarations describe the addresses to provide to clients.

Parameters and declarations entered into the dhcpd.conf file (Figure 7–11) generally start with the word *option*. The configuration file can contain tabs or blank lines to make it easier to read. All keywords are case-insensitive, and lines beginning with a pound sign (#) are comments. Available options can be viewed with the man *dhcp-options* command. Some of the options for dhcpd.conf are:

- `option domain-name name;` Specifies the domain name that clients should use when resolving hostnames with DNS.
- `option domain-name-servers <ip-address>, <ip-address>. . .;` The DNS available to clients. The DNS IP addresses should be listed in order of preference.
- `option routers <ip-address>, <ip-address>. . .;` Specifies a list of IP addresses for routers on the client’s subnet. Routers should be listed in order of preference.
- `option subnet-mask <ip-address>;` Specifies the client’s subnet mask.
- `default-lease-time number-of-seconds;` The length of time the lease is valid.
- `max-lease-time <number-of-seconds>;` The maximum of time in seconds that the server will grant a lease.
- `range <low-ip-address> <high-ip-address>;` The range of IP addresses to assign to clients.

![](img/37f079cee226b270f2e09b37a2e4a05d_186_0.png)

To start DHCP (Figure 7-12), enter the command

```bash
service dhcpd start
```

If you make changes to the dhcpd.conf file, you must restart the service with the command

```bash
service dhcpd restart
```

FIGURE 7-12 dhcpd start.

![](img/37f079cee226b270f2e09b37a2e4a05d_187_0.png)

The lease database, /var/lib/dhcp/dhcpd.leases, stores the DHCP client leases. This file is dynamically changed by the dhcpd process as clients request configuration information. If the lease database file does not exist, it can be created with the touch command. The touch command updates the access and modification times of an existing file. If the file does not exist, the file is created. To create the /var/lib/dhcp/dhcpd.leases file, type `touch /var/lib/dhcp/dhcpd.leases`.

### Objective 3.1 DHCP Client

After configuring the DHCP server, the clients must be configured. Different hosts on the network are configured in different ways to access DHCP. The two most commonly used clients are Linux and Windows. To configure a DHCP Linux client, you must modify two files. The /etc/sysconfig/network file enables networking and the /etc/sysconfig/network-scripts/device-name (where device-name identifies the device to configure) file enables parameters for a specific device. The /etc/sysconfig/network file should have the following line:

```bash
NETWORKING=yes
```

This line indicates that networking is enabled. Typically, a system will have one Ethernet adapter, though two Ethernet adapters are not uncommon. The first Ethernet adapter is identified as eth0. The file containing configuration for the first Ethernet adapter is /etc/sysconfig/network-scripts/ifcfg-eth0. For DHCP, this file should contain the following entries:

```bash
DEVICE=eth0
BOOTPROTO=dhcp
ONBOOT=yes
```

The versions of Windows that are typically in use are numerous. All versions are configured similarly. The client configured here is Windows XP.

To configure DHCP on Windows XP, select **Network Connections** from the Control Panel. (The Control Panel can be accessed from the Start menu on the Taskbar.) The Network Connections window (Figure 7–13) is displayed.

![](img/37f079cee226b270f2e09b37a2e4a05d_188_0.png)

From the Network Connections window, right-click the Local Area Connection icon and then select **Properties** from the pop-up menu. The Local Area Connection Properties dialog box (Figure 7–14) is displayed.

![](img/37f079cee226b270f2e09b37a2e4a05d_188_1.png)

Select **Internet Protocols (TCP/IP)** from the list box, **This connection uses the following items:**, then select the **Properties** button. The Internet Protocol (TCP/IP) Properties dialog box (Figure 7–15) is displayed.

![](img/37f079cee226b270f2e09b37a2e4a05d_189_0.png)

Ensure that the option buttons **Obtain an IP address automatically** and **Obtain DNS server address automatically** are selected.

Select the **OK** button to close the dialog boxes and then close the windows that are opened. The DHCP client is now ready.

## Static Configuration

Objective 3.7

Configuring your computer with a static IP address is necessary on some networks. On some networks, static addresses are used to improve security. If IP addresses are not assigned automatically, someone tapping into the network would have to acquire the network address and the subnet mask to use the network. Servers are typically assigned a static address to ensure that their services are provided from a consistent address.

Using static addresses does not require setting a server; however, the Ethernet adapter must be configured. If the system will be connecting to other networks the gateway must be set. If the system will use DNS, it must be configured as well.

The properties that must be set to use networking are:

- Host IP address
- Host subnet mask
- Gateway IP address
- DNS server(s) IP address
- Host name
- Domain name

### Host IP Address and Subnet Mask

Static values for the client are set on the Ethernet adapter(s). To set a static address on the eth0 adapter, you can use the **ifconfig** command. The ifconfig command is also used to display the current configuration of network interfaces. The syntax of ifconfig is **ifconfig interface options**. For a complete list of options, use **man ifconfig**. Some valid options are:

- `up` Activates the network interface.
- `down` Shut down the network interface.
- `netmask <address>` Set the subnet mask.
- `<address>` The IP address of the network interface.

To set the first Ethernet interface with an address of 192.168.0.20 and a subnet mask of 255.255.255.0, use the following command:

`ifconfig eth0 192.168.0.20 netmask 255.255.255.0`

These properties are contained in the file **/etc/sysconfig/network-scripts/ifcfg-eth0**. This file can be edited directly.

### Hostname and Gateway

The hostname and gateway can be set in the **/etc/sysconfig/network** file. Besides the NETWORKING entry, the /etc/sysconfig/network file can have the following entries:

- `HOSTNAME=<value>` The value is a Fully Qualified Domain Name (FQDN), such as *LinuxServer.linuxplus.com*.
- `GATEWAY=<value>` The value is the IP address of the network's gateway.

To configure a hostname of myserver on domain linuxplus.com with the gateway address 192.168.0.1, place the following entries in the **/etc/sysconfig/network** file.

```bash
NETWORKING=yes
HOSTNAME=myserver.linuxplus.com
GATEWAY=192.168.0.1
```

### DNS Server and Domain Name

Domain names are resolved to IP addresses to be used on the Internet. To resolve the addresses you have to have the IP address of a local name server (DNS) that you can use. To configure the DNS server, you need to edit three files.

**/etc/resolv.conf**
The /etc/resolv.conf file is the main configuration file for the name resolver. Three keywords are typically used by the file. View all the available options with the **man resolv.conf** command.

- `domain <value>` The value is the domain name to append to unqualified names. For example, if the hostname is smithcomputer, not an FQDN, the domain is appended to the hostname.
- `search <value>` The value is a list of alternate domain names to search for a hostname.
- `name server <ip_address>` Enter the IP address of a DNS server to query when resolving names. There can be several name server entries for multiple DNS servers.

If the host name is myserver and the name servers are at IP addresses 192.168.0.250 and 192.168.0.251, the following entries would be in the /etc/resolv.conf file:

```bash
domain linuxplus.com
search linuxplus.com
name server 192.168.0.250
name server 192.168.0.251
```

**/etc/host.conf**
This file contains configuration information specific to the resolver library. Two keywords need to be configured for most instances, order and multi. Other keywords can be found by using the **man host.conf** command.

- `order <value>` The value specifies how host lookups are to be performed. The value can contain bind, hosts, and nis. hosts means to use the /etc/hosts file.
- `multi <on/off>` If set to on, the resolver library will return all valid addresses for a host from the /etc/hosts file.
