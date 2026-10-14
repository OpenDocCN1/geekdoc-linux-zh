
## DHCP Software Packages

SuSE Linux comes with three packages related to DHCP, all included in series N. The first of these is the DHCP server `dhcpd` distributed by the Internet Software Consortium, or ISC. This is the program that assigns and manages the corresponding information for the network. Normally with SuSE Linux, there is only this one program available as far as the server is concerned, but you can choose between two different DHCP client programs. SuSE Linux includes both the package `dhclient`, also from the ISC, and the “DHCP client daemon” provided by the package `dhcpcd`.

SuSE Linux installs `dhclient` by default. The program is very easy to handle and will be launched automatically on each system boot to watch for a DHCP server. It does not need a configuration file to do its job and should work out of the box in most standard setups.

If you administer a more complex network, you might need the ISC’s `dhclient`, which can be controlled via the configuration file `/etc/dhclient.conf`. No matter whether you want to include an additional domain in the search list or even to emulate the behavior of a Microsoft DHCP client — if you are knowledgeable about networks, you will find that the `dhclient` gives all the possibilities to make it function according to your needs, down to the last detail.

## The DHCP Server dhcpd

The core of any DHCP system is the *dynamic host configuration protocol daemon*. This server “leases” addresses and watches how they are used, according to the settings as defined in the configuration file `/etc/dhcpd.conf`. By changing the parameters and values in this file, a system administrator can influence the program’s behavior in numerous ways. Look at a basic sample `/etc/dhcpd.conf` file:

```conf
default-lease-time 600;        # 10 minutes
max-lease-time 7200;            # 2 hours

option domain-name "kosmos.all";
option domain-name-servers 192.168.1.1, 192.168.1.2;
option broadcast-address 192.168.1.255;
option routers 192.168.1.254;
option subnet-mask 255.255.255.0;

subnet 192.168.1.0 netmask 255.255.255.0
{
    range 192.168.1.10 192.168.1.20;
    range 192.168.1.100 192.168.1.200;
}
```

*File 57: The Configuration File /etc/dhcpd.conf*

This simple configuration file should be sufficient to get the DHCP server to assign IP addresses to the hosts of your network. One thing to remember, however, is to include a semicolon (;) at the end of each line. Without that character, dhcpd will not even start.

As you might have noticed, the above sample file can be subdivided into three different sections. The first one defines how many seconds an IP address is “leased” to a requesting host by default (default-lease-time) before it should apply for renewal. The section also includes a statement on the maximum period for which a machine may keep an IP address assigned by the DHCP server without applying for renewal (max-lease-time).

In the second part, some basic network parameters are defined on a global level:

- The line option `domain-name` defines the default domain of your network.
- With the entry option `domain-name-servers`, specify up to three values for the DNS servers used to resolve IP addresses into host names (and vice versa). Ideally, configure a name server on your own machine or somewhere else in your network before setting up DHCP. That name server should also define a host name for each dynamic address and vice versa. To learn how to configure your own name server, read Section DNS — *Domain Name Service* on page 349.
- The line option `broadcast-address` defines the broadcast address to be used by the requesting host.
- With option `routers`, tell the server where to send data packets that cannot be delivered to a host on the local network (according to the source and target host address and the subnet mask provided). In most cases, especially in smaller networks, this router will be identical with the Internet gateway.
- With option `subnet-mask`, specify the netmask assigned to clients.

The last section of the file is there to define a network, including a subnet mask. To finish, specify the address range that the DHCP daemon should use to assign IP addresses to interested clients. In our example, clients may be given any address between `192.168.1.10` and `192.168.1.20`, as well as `192.168.1.100` and `192.168.1.200`.

After editing these few lines, you should be able to activate the DHCP daemon by issuing the command `rcdhcpd start`. The server is ready for use immediately after that. Do a basic check to see whether the configuration file is syntactically correct by entering the command `rcdhcpd syntax-check`. If you encounter any unexpected problems with your configuration — the server aborts with an error or does not return “done” on start — you should be able to find out what has gone wrong by looking for information either in the main system log `/var/log/messages` or on console 10 (Ctrl + Alt + F10).

## Assigning Fixed IP Addresses to Hosts

Now that the server is set up to assign dynamic addresses, it is time to have a closer look at static addresses and the way to configure them. As mentioned above, with DHCP it is also possible to assign a predefined, fixed address to one host each time the latter sends a request to the server. As might be expected, addresses assigned explicitly will always take priority over addresses from the pool of dynamic addresses. Furthermore, a static address will never expire in the way a dynamic address would, such as if there were not enough addresses available so the server needed to redistribute them among hosts.

To identify a host configured to get a static address, the DHCP daemon fetches the hardware address of that host. This is a numerical code consisting of six octet pairs, fixed in most cases, and unique to each network device sold in the world, e.g., `00:00:45:12:EE:F4`.

If the appropriate lines, like the ones in 58, are added to the configuration file 57 on page 369, the DHCP daemon will assign the same set of data to the corresponding host under all circumstances.

```
host earth {
    hardware ethernet 00:00:45:12:EE:F4;
    fixed-address 192.168.1.21;
}
```

### *File 58: Entry Added to the Configuration File*

The structure of this entry should be almost self-explanatory: The first line sets the DNS name of the newly defined host (host *host name*) and the second one its MAC address. On any network-enabled Linux host, this address can be determined very easily with the command *ifconfig* plus the network device, for example, eth0. If the network card is not enabled, use the command *ifup eth0* first. The output should contain something like *link/ether 00:00:45:12:EE:F4*.

In the above example, a host with a network card having the MAC address *00:00:45:12:EE:F4* is assigned the IP address *192.168.1.21* and the host name *earth* automatically.

The type of hardware to enter is ethernet in nearly all cases, though token-ring, which is often found on IBM systems, is also supported.

## The Finer Points

As stated at the beginning of this chapter, these pages are only intended to provide a brief survey of what you can do with DHCP. For more information, the page of the *Internet Software Consortium* on the subject (http://www.isc.org/products/DHCP/) will prove a good source to read about the details of DHCP, including about version 3 of the protocol, currently in beta testing. Apart from that, you can always rely on the man pages for further help. Try man dhcpd, man dhcpd.conf, man dhcpd.leases, and man dhcp-options. Also, several books about *Dynamic Host Configuration Protocol* have been published over the years that take an in-depth look at the topic.

With dhcpd, it is even possible to offer a file to a requesting host, as defined with the parameter *filename*, and that this file may contain a bootable Linux kernel. This allows you to build client hosts which do not need a hard disk — they are enabled to load both their operating system and their network data over the network (*diskless clients*), which could be an interesting option for both cost and security reasons. Now add the package alice to all this and you can do some really amazing things.
