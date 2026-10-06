
## 728 Linux Administration: A Beginner's Guide

dynamic-boot-lease-cutoff BOOT clients are not aware of the lease concept. By default, the DHCP server assigns an IP address that never expires. In certain situations, it may be useful to have the server stop issuing addresses for a set of BOOT clients. In these cases, this parameter is used. This parameter's syntax is as follows:

```
dynamic-boot-lease-cutoff date;
```

The date is specified in the form W YYYY/MM/DD HH:MM:SS, where W is the day in cron (0–Sunday, 6–Saturday), YYYY is the year, MM is the month (01=January, 12=December), DD is the two-digit format, HH is the two-digit hour in 24-hour format (0=Midnight, 23=p.M.), MM is the two-digit representation of minutes, and SS is seconds.

dynamic-boot-lease-length Although the BOOT clients don't have a mechanism for expiring the addresses they receive, it's sometimes to save the server assume that they aren't using the address anymore, freeing it for further use. This is useful if the BOOT application is known to be short in duration. If so, the server can set the number of seconds and expire it after that time has passed.

```
dynamic-boot-lease-length seconds;
```

> CAUTION Use the dynamic-boot-lease-length parameter with caution, as it can introduce problems if it issues an address before another host has stopped using it.

filename In some applications/environments, the DHCP client may need to know the name of a file to use boot. This is often combined with next-server to retrieve a remote file for installation configuration or diskless booting. This parameter's syntax is as follows:

```
filename filename;
```

fixed-address or fixed-address6 This parameter is only applicable under the host declaration. It specifies the set of addresses (IPv4 or IPv6) assignable to the client. This parameter's syntax is as follows:

```
fixed-address address [, address];
fixed-address ip6-address [, ip6-address];
```

get-lease-hostnames If this parameter is set to true, the server will resolve all addresses in the declaration space and use that for the hostname option. This parameter's syntax is as follows:

```
get-lease-hostnames [true | false];
```

## CHAPTER 29 Dynamic Host Configuration Protocol (DHCP) 72

hardware For a BOOTP client to be recognized, its network hardware address must be declared using a hardware clause in the host statement. This parameter’s syntax is as follows:

```
hardware-type hardware-address;
```

Here, hardware-type must be the name of a physical hardware interface type. Currently, only the Ethernet and Token Ring types are recognized. The hardware-address (sometimes referred as the media access control, or MAC, address) is the physical address of the interface, typically a set of hexadecimal octets delimited by columns. The hardware statement can also be used for DHCP clients.

max-lease-time A client has the option to request the duration of the lease. The request is granted as long as the lease time doesn’t exceed the number of seconds specified by this option. Otherwise, the client is granted a lease to the maximum of the number of seconds specified here. This parameter’s syntax is as follows:

```
max-lease-time seconds;
```

next-server The next-server statement is used to specify the host address of the server from which the initial boot file (specified in the filename statement) is to be loaded. This parameter's syntax is as follows:

```
next-server server-name;
```

Here, server-name is a numeric IP address or a domain name.

server-identifier Part of the DHCP response is the address for the server. On Multi-homed systems, this interface may not be reachable by all clients of a server or declaration scope. In those rare instances, this parameter can be used to send the IP address of the proper interface that the client should communicate to the server. The value specified must be an IP address for the DHCP server, and must be reachable by all clients served by a particular scope. This parameter’s syntax is as follows:

```
server-identifier hostname;
```

server-name The server-name statement can be used to inform the client of the name of the server from which it is booting. This parameter is sometimes useful for remote clients or network installation applications. This parameter’s syntax is as follows:

```
server-name Name;
```

Name should be the name that will be provided to the client.

use-lease-addr-for-default-route Some network configurations use a technique known as Proxy ARP so that a host can keep track of hosts that are outside its subnet. If your network is configured to support ARP, you'll want to configure your client to use itself as a default route. This will force it to use ARP (Address Resolution Protocol) to find all remote (off the subnet) addresses. This parameter's syntax is as follows:

```
use-lease-addr-for-default-route [true|false];
```

> CAUTION The use-lease-addr-for-default-route command should be used with caution. Not every client can be configured to use its own interface as a route.

## Options

Currently, the DHCP server supports more than 60 options. The general syntax of option is as follows:

```
option option-name [modifiers]
```

Table 29-1 summarizes the most commonly DHCP options.

| Option | Description |
| :--- | :--- |
| broadcast-address | An address on the client's subnet specified as the broadcast address |
| domain-name | The domain name the client should use as the local domain when performing lookups |
| domain-name-servers | The list of Domain Name System (DNS) servers for the client to use to resolve hostnames |
| host-name | The string used to identify the client |
| nis-domain | The name of the client's NIS (Network Information Services) domain |
| nis-servers | A list of available NIS servers to the client |
| routers | A list of IP addresses for the client to use, in order of preference |
| subnet-mask | The netmask the client is to use |

## CHAPTER 29 Dynamic Host Configuration Protocol (DHCP) A Sample dhcpd.conf File

The following is an example of a simple configuration file:

```
subnet 192.168.222.0 netmask 255.255.255.0 {
  # Options
  option routers 192.168.222.1;
  option subnet-mask 255.255.255.0;
  option domain-name "example.org";
  option domain-name-servers ns1.example.org;
  # Parameters
  default-lease-time 21600;
  max-lease-time 43200;
  # Declarations
  range 192.168.222.25 192.168.222.49;
  # Nested declarations
  host client {
    hardware 00:80:c6:f6:72:00;
    fixed-address 192.168.222.50;
  }
}
```

In this example, note the following:

- A single subset is defined. The DHCP clients are instructed to use 192.168.222.1 as their default router (gateway address) and 255.255.255.0 as their subnet mask.
- DNS information is passed to the clients; they will use example.org as their domain name and ns1.example.org as their DNS server.
- A lease of 21600 seconds is set, but if the clients request a longer lease, they may be granted as long as 43200 seconds.
- The range of IP addresses issued at 192.168.222.25 can go as high as 192.168.222.49. The machine with MAC address of 00:80:c6:f6:72:00 will always get the IP address 192.168.222.50.

To set up your DHCP server with the sample configuration, all you need to create/edit a file /etc/dhcp/dhcpd.conf and populate the file with the entries in our sample file.

We've thoughtfully (we're nice like that!) bundled working copies of the configuration and/or scripts used in this chapter at the following URL to save you typing:

http://linuxserverexperts.com/7/chapter-29.tar.xz

To follow along this bundle, download the file (wget URL), extract its contents (decompress it using tar xvJf chapter-29.tar.xz), and copy the file(s) to the proper directories on your local system.

## 732 Linux Administration: A Beginner's Guide

> CAUTION It is of paramount importance that you make sure that your DHCP server has at least one network interface configured with an IP address that belongs to the same network as the network defined in the subnet declaration of the dhcp.conf file. This means, for example, that you shouldn't have a subnet declaration that reads subnet 192.168.222.0 mask 255.255.255.0 while your DHCP server has a single network interface (such as eth0) with an IP address of 172.16.0.10.

You should also ensure that the IP address of the DHCP server is excluded from the network range of issued/leased IP addresses specified in the range declaration. The DHCP server in our example should have a static IP address that lies in the range 192.168.222.1 to 192.168.222.24. If you ignore this warning, the dhcp server will fail with errors similar to any of these:
No subnet declaration for eth0 ((current-ip-address)).
Not configured to listen on any interfaces!
Failed to start DHCP Server Daemon.

## Starting and Stopping dhcpd

On system-enabled Linux distributions, you can use the systemctl utility to query the status of the dhcp daemon and to manage the service.
Begin by checking if the service is:

```
[root@server ~]# systemctl status dhcpd.service
```

If the output shows that the service is not running (inactive, dead, and so on), use the start option with the systemctl utility to start the service:

```
[root@server ~]# systemctl start dhcpd.service
```

If you've made some dhcp.conf configuration changes and you want the running dhcpd server instance to include/implement your changes, you can restart the server by running

```
[root@server ~]# systemctl restart dhcpd.service
```

To stop the dhcpd service, type

```
[root@server ~]# systemctl stop dhcpd.service
```

# General dhcpd Runtime Behavior

Once it's started, the daemon patiently waits for a client request prior to performing any processing. When a request is processed and an address is issued, the daemon keeps track of the address in a file called dhcpd.leases. On Fedora, RHEL, and CentOS systems, this file is stored in the /var/lib/dhcpd/ directory.
