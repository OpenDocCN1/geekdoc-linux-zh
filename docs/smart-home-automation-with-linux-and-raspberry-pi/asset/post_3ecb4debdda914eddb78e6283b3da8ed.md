
I’ll cover various media-oriented head units in Chapter 3, although most of those shown could be re-created with a Linux machine running the appropriate software. However, the power usage, noise, and cost will generally be larger than a custom-built embedded device, even though many of those devices may be running Linux themselves! To connect the units, however, you need to know how to set up a network.

## Networking Primer

To best utilize the devices here, you will need to configure a Linux machine as a suitable server. Most computer science books will begin their networking section by describing the OSI seven-layer model of networking . . . I won’t! Instead, you’ll learn only the necessary, practical steps of providing and configuring a suitable home network for automation.

> **Note**  Each Linux example here, and throughout the book, is based around Debian and the packages within it.
> 
> This is not advocacy on my part, merely practicality, because it’s what I use. Some distributions may place the files in slightly different places or have slightly different names, but the principles are always the same, and the equivalents are easy to find.

## Concepts

A home network is a way for each computer in the house to share a set of common resources such as printers, scanners, and storage space. In this sense, it’s very much like an office network. Where the home differs is in the level of technology and, consequently, the expertise needed to run it. One of the main bugbears in office IT systems is the issue of security. With a home network, the relationships between the people using it are very much different, and social mores are brought to bear.

The standard network configuration has two parts—internal and external. The *internal* part is a network that connects all the house computers together, along with their peripherals, and makes them invisible to the outside world. These devices may be networked together through cables or wireless.

The *external* network is everything else! The big, wide Internet is generally unavailable to the computers at home; it is available only by connecting to an ISP through a modem, broadband connection, 3G card, or similar device.

To connect these two sides of the network together, you need a router. Sometimes the router is a small box that comes as part of your DSL/cable/broadband package and automatically separates the internal and external traffic. Sometimes you’ll need to buy one. They have one RJ-45 socket carrying the external network traffic, into which you plug the network cable from the broadband modem, and one or more outputs to the internal network.

Alternatively, you can use a PC with two network cards—one configured to talk to the external network and one for the internal. If you have a 3G card, then this acts like your externally configured network card.

With the router existing in both internal and external networks, it is able to automatically keep both sets of traffic separate and block any data or software you don’t want moving between the two. Most routers are configured, by default, to allow all outgoing traffic but block all incoming traffic, except those on specific ports. The port is the route by which traffic protocols flow and is referenced by a number. All web pages, for example, are requested on port 80. So if your router is blocking incoming traffic on port 80, you won’t be able to access your internal web server from outside your home’s internal network.

Depending on the number of machines on your network, you might also need a switch that provides additional network sockets, into which you can plug more computers. Although it is unlikely that many people will fill eight sockets with computers, it is not uncommon to have non-computer devices that also use Ethernet to transmit data, thereby exhausting the available sockets.

## Addressing

Every device on the network must have a unique address. There are two current forms of addressing, IPv4 and IPv6. IPv4 was the original form of describing addresses by means of a dotted quad, such as 89.16.172.66, and is used by virtually every machine and home device on the planet. IPv6 was introduced in 1998 by the Internet Engineering Task Force to overcome the various problems with IPv4, such as address exhaustion. However, its adoption is less than widespread, and many of the small, home-oriented devices do not use it, so I’ll be concentrating on IPv4.

For a machine to have an address, it must be given one, either by a human or by a suitably configured computer. It cannot randomly generate one in case the address conflicts with another machine on the network or is one of the reserved addresses, such as 127.0.0.1. All the networked machines in the home should exist within a specific range of addresses, known as a subnet, and should be assigned to one of the private address ranges provided by the IPv4 specification. This not only stops conflicts with other existing sites on the Internet but also ensures the data within these networks is secure and invisible to machines outside the network, because all routers, switches, and gateways do not recommunicate any traffic with a private address range outside the local network. These private address ranges are 10.x.x.x, 172.16-31.x.x, and 192.168.x.x⁹, where x can mean any value between 0 and 255. For the purposes of demonstration, I will assign my subnet to the 192.168.1.x range, giving me 254¹⁰ possible devices on the network. Most people use this for private networks because nearly all the routers sold for the home allocate addresses within this range. Also, most questions found on the various Internet forums will probably have answers detailed using the same addresses as you have.

Now knowing the address range of your network, you have to consider the individual addresses. The first one to assign is the router, which usually earns the 192.168.1.1 designation,¹¹ followed by the Linux server, which I will assign 192.168.1.2.

> **Caution**  Configuring properties such as IP addresses requires you to be logged in as root, so tread carefully!

You can provide a Linux machine a static address either by using the tools in your desktop GUI or by configuring the /etc/network/interfaces file directly:

```text
auto eth1
iface eth1 inet static
        address 192.168.1.2
        netmask 255.255.255.0
        broadcast 192.168.1.255
        network 192.168.1.0
```

This tells the system to use the network card assigned as eth1¹² for the static IPv4 address 192.168.1.2, with all the standard parameters.

⁹ You might also see this listed as 10.0.0.0/8, with the 8 indicating that the first 8 of 32 binary digits within the address are fixed resulting in a range of over 16 million addresses between 10.0.0.0 through 10.255.255.255. Similarly, you might also see the following in use: 172.16.0.0/12 (providing a range of over 1 million addresses between 172.16.0.0 through 172.31.255.255) and 192.168.0.0/16 (providing a range of 65,536 addresses between 192.168.0.0 through 192.168.255.255).
¹⁰ There are two addresses reserved for the subnet (0) and broadcast (255), thus reducing the total number from 256 to 254.
¹¹ Some routers can not be configured away from 192.168.1.1, so it’s best to avoid using this number for anything else.
¹² Determine whether this is eth0 or eth1 by either checking the output of dmesg | grep eth or adding the alias eth1 mynetcarddevice to /etc/modules.

You *can* use this approach to assign static IPv4 addresses to every machine on your network—simply make note of which machine is given which number. However, this can become tiresome after a while, and many embedded devices don’t allow such control over the configuration. Either case requires you to upgrade to DHCP.

DHCP stands for Dynamic Host Configuration Protocol and is a way of configuring the networking facilities of each client machine on the network. The software comes in two parts, a client and a server. The client says simply, “I’m a machine; where is the network?” by transmitting a message onto the cable for all machines to hear. The server listens for any and all of these messages and responds by returning all the configuration data that the sender should use for networking, such as its IPv4 address, domain name, and so on.

Configuring a DHCP client in Linux is easy and involves replacing the earlier section of the `/etc/network/interfaces` file with the following:

```text
auto eth1
iface eth1 inet dhcp
```

Creating a DHCP server takes a little more work but can often be avoided as many network routers include one, although it’s sometimes disabled by default.

To prepare one in Linux, you should first install the DHCP server software with a command such as this:

```text
apt-get install dhcp3-server
```

You can then edit the `/etc/dhcpd.conf` file to assign addresses to each machine. Prior to editing, you may need to run this:

```text
ln -s /etc/dhcp3/dhcpd.conf /etc/dhcpd.conf
ln -s /usr/sbin/dhcpd3 /usr/sbin/dhcpd
```

The addresses of each machine can be assigned by following these steps:

1. Giving it the next free number in a series, say 100–254. These are pooled addresses.
2. Looking at the MAC address of the network card that sent the message (all MACs are unique) and giving it a specific address based on that number.
3. Doing any combination of 1 and 2.

Because these pooled addresses are finite in number, they are never *given* to a machine. Instead, they are *leased*, and the DHCP client of each machine must request the address if it’s still using it after a certain amount of time. The software does this automatically behind the scenes. If you have a lot of visitors to your home (who’d rather use the Internet than talk with you!), then leasing addresses is the simplest way to go because each friend wouldn’t need to have a static address that would require configuration.

Pooled addresses are configured like this:

```text
subnet 192.168.1.0 netmask 255.255.255.0 {
    option routers        192.168.1.1;
    range 192.168.1.5 192.168.1.115;
}
```

Otherwise, the number of machines in your house is probably limited, so static addresses add very little work and make it quicker to troubleshoot since you know in advance what IP each computer should have. A typical configuration would appear like this:

```text
host teddys-pc {
    hardware ethernet 00:A1:68:8E:9E:AA;
    fixed-address 192.168.1.4;
}
```
