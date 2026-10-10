
is not working and will step through the actions needed. This is especially important where multiple network cards are installed. With multiple NICs, the cards are sequentially numbered eth0, eth1, and so forth, and you must be sure that you are manipulating the correct device.

The NIC must be turned on for the system to recognize it, and you can achieve this using the command:

```
ifconfig eth1 up
```

or alternatively:

```
ifup eth1
```

Reconfiguring the IP and subnet mask of the device may require the NIC to be inactive or to be turned on and off. This can be achieved using `ifconfig` or `ifdown`, as such:

```
ifconfig eth1 down
ifdown eth1
```

### Exam Warning

> Remember that `ifconfig`, `ifup`, and `ifdown` are usually located in the `/sbin` directory, which is not part of the path as defined in `$PATH` for most users. The full directory path may therefore be required to execute the commands.

Some older NICs require the card to be set to specific IRQ and I/O addresses, and these can be set by the `ifconfig` command as well. Most modern NICs will be autodetected by the kernel, and hence this step will not be required.

```
ifconfig eth1 irq 12 io_addr 0x300
```

Once these commands are undertaken, the execution of the `ifconfig` command with no parameters should display the newly set up NIC. The IP address associated with the NIC can be assigned dynamically from a DHCP server [more details are given later in the chapter in the section “DHCP Set Up and Configuration”], or it can have a static address assigned to it. It is more common to assign a static address to servers, particularly if they are Internet-facing. To set a NIC to a specific IP address, the command is

```
ifconfig eth1 10.10.10.3 netmask 255.255.255.0
```

The `ifconfig` command should be run again to display the status of the NIC and to ensure that the IP address has been set correctly.

## DHCP Setup and Configuration

For the majority of devices, the use of DHCP will be the preferred option. For small networks, these addresses are often obtained from the broadband router or similar device. For larger corporations, the use of DHCP is preferred to reduce the support and maintenance overhead of using static addresses.

The host running DHCP obtains an IP address by contacting a central server, which maintains the addresses for one or more subnets. Once the client has contacted the server, it will be assigned an IP address, subnet mask, and potentially other information such as the default route and IP address of the default name server. The information that is requested is listed in the configuration file `/etc/dhclient.conf` and is read upon startup, and will attempt to configure all the interfaces that are present on the system. The default is to require only the IP address configuration, although the domain name servers (DNSes) can also be required if the appropriate line is defined in the dhclient file.

A command-line DHCP client can also be used to configure the network interface, called `dhcpd`, which is located in the `/etc` directory. The DNS information obtained from the server will be written to the `resolvconf` or, if unavailable, directly to `/etc/resolv.conf`. In larger networks, the DHCP server may also supply configuration data for NFS and Network Time Protocol (NTP), and these will be stored in `/etc/yp.conf` and `/etc/ntpd.conf`. These services will also be stopped and started by `dhcpd` to ensure they are notified of the change.

For support reasons, a number of other options are useful with the `dhcpd` command:

- `--release` releases the current lease from the host and deconfigures the interface.
- `--renew` will attempt to renew the lease. These two commands are often done sequentially to check the connection to the DHCP server.
- `--nogateway` will restrict any duplication of the default route.
- `--nonntp` will stop the ntp being updated in `/etc/ntp.conf`
- `--nodns` is used to stop the DNS information being updated in `/etc/resolvconf`

A DHCP alternative client is `dhclient`, which runs on startup and reads the `/etc/dhclient.conf` file to read its configuration instructions. This file will contain a list of all the network interfaces that are configured in the current system. These will, if necessary, be configured with the dhclient. If the interface is configured using this client, it stores the DHCP lease in the `/var/lib/dhcp/dhclient.leases` configuration file. As the number of leases may be large, this file is recreated from time-to-time to ensure a manageable size.

## Configuring a Wireless Interface

The use of wireless network cards has grown rapidly over the last few years due to the increase in speed of the wireless infrastructures. The configuration of a wireless interface is very similar to that of a wired interface. To display the status of all the wireless interfaces on a system, `iwconfig` is used with no parameters or the `iwlist` command, which is found in `/usr/sbin`. The wireless statistics are obtained from the `/proc/net/wireless` file.

To set up a wireless NIC, the main parameters to be used are given below:

- ESSID is used to set the network name to enable the user to roam across a number of access points.
- mode will need to be set depending on the network topology. The common parameters are managed for a network of many access points, ad hoc for a point-to-point connection, and master if the device will act as access point.
- key/enc is used to set the current encryption key, and is entered in hex notation in the form XXXX-XXXX-XXXX-XXXX or as an ASCII string with the `s:` prefix.

## Network Configuration Files

There are a number of network configuration files in the systems that are modified automatically or manually. The files can have comments embedded in them using the # symbol as per normal, and it is advisable to add meaningful comments if these files are modified manually.

### Hosts File, /etc/hosts

The hosts file maps actual IP addresses to hostnames. For large networks, this is usually undertaken by using DNS, as the maintenance involved in keeping hosts files current is usually large. The hosts file will contain both IPv4 and IPv6 addresses. Often, it is useful to add a small number of frequently used hosts into the hosts file to reduce the load on the network and name servers.

### Services, /etc/services

The services file maps port numbers to services. A port is specific to an application and is the communication endpoint used by the transport layer protocols in the IP suite. Applications will use these port numbers to ensure that the sending and receiving systems understand which application the packet is destined for. For example, suppose a host wishes to display a Web page located on another system. The standard port for the World Wide Web Hypertext Transport Protocol [HTTP] is 80, so the source will send a packet to destination with port 80 in the IP header block. The destination will then know to route the packet to the Web server application to execute. On a typical system, it is not necessary to modify the services file after it has been initially configured during installation.

### Name Switch Service, /etc/nsswitch.conf

The Name Switch Service is used to tell the system which service to use, with potentially a number of entries per service to allow for multiple “databases” and their lookup order to be specified. Typically, there will be entries for passwd, hosts, networks, and services – among others. The typical entries are as follows:

- `nis` – use NIS or YP
- `dns` – use the domain name service
- `files` – use the local files

Typical entries would look like:

```
hosts:      files dns
netmasks:   files
netgroup:   files nis
```

### Resolver File, /etc/resolv.conf

The resolv.conf file will normally be constructed automatically and will never need to be changed manually. It will contain the list of one or more name-servers, typically obtained from the DHCP service. The list of servers will be defined such as:

```
nameserver 68.87.85.98
nameserver 68.87.69.146
```

### TCP/IP Ports

There are a number of common networking ports that are used frequently. The entire list is very long and is organized into a number of sections. Ports 0 through 1023 are defined as well-known ports, such as FTP. Registered ports, that is those with an Internet Assigned Numbers Authority [IANA] registration, are from 1024 through 49151. The remainder of the ports from 49152
