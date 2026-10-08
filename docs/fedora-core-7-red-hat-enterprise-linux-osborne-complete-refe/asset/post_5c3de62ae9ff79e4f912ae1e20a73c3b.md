
servers or name servers). These DNS servers keep lists of fully qualified domain names and their IP addresses, matching one up with the other. This service that they provide to a network is referred to as the Domain Name System. The Internet is composed of many connected subnets called *domains*, each with its own DNS servers that keep track of all the fully qualified domain names and IP addresses for all the computers on its network. DNS servers are hierarchically linked to root servers, which, in turn, connect to other root servers and the DNS servers on their subnets throughout the Internet. The section of a network for which a given DNS server is responsible is called a *zone*. Although a zone may correspond to a domain, many zones may, in fact, be within a domain, each with its own name server. This is true for large domains where too many systems exist for one name server to manage.

## DNS Operation

When a user enters a fully qualified domain name to access a remote host, a resolver program queries the local network’s DNS server requesting the corresponding IP address for that remote host. With the IP address, the user can then access the remote host. In Figure 36-1, the user at **rabbit.mytrek.com** wants to connect to the remote host **lizard.mytrek.com**. rabbit.mytrek.com first sends a request to the network’s DNS server—in this case, **turtle.mytrek.com**—to look up the name lizard.mytrek.com and find its IP address. turtle.mytrek.com then returns the IP address for **lizard.mytrek.com, 192.168.0.3**, to the requesting host, rabbit.mytrek.com. With the IP address, the user at rabbit.mytrek.com can then connect to lizard.mytrek.com.

## DNS Clients: Resolvers

The names of the DNS servers that service a host’s network are kept in the host’s *etc/resolv.conf* file (see Chapter 35). When setting up an Internet connection, the name servers provided by your Internet service provider (ISP) were placed in this file. These name servers resolve any fully qualified domain names that you use when you access different Internet sites.

### FIGURE 36-1
DNS server operation

![](img/ab68ea377332b50bf70ef1316c8175b6_864_0.png)

For example, when you enter a Web site name in your browser, the name is looked up by the name servers and the name's associated IP address is then used to access the site.

#### /etc/resolv.conf

```
search mytrek.com mytrain.com
nameserver 192.168.0.1
nameserver 192.168.0.3
```

## Local Area Network Addressing

If you are setting up a DNS server for a local area network (LAN) that is not connected to the Internet, you should use a special set of IP numbers reserved for such local networks (also known as *private networks* or *intranets*). This is especially true if you are implementing IP masquerading, where only a gateway machine has an Internet address, and the others make use of that one address to connect to the Internet. Though structurally the same, IPv4 and IPv6 use different addressing formats for local addresses. Many local and home networks still use the IPv4 format, and this is the format used in the following local addressing example.

### IPv4 Private Networks

IPv4 provides a range of private addresses for the three classes supported by IPv4. As you have seen, class C IPv4 network numbers have the special network number 192.168. Numbers are also reserved for class A and class B non-Internet local networks. Table 36-1 lists these addresses. The possible addresses available span from 0 to 255 in the host segment of the address. For example, class B network addresses range from 172.16.0.0 to 172.16.255.255, giving you a total of 65,534 possible hosts. The class C network ranges from 192.168.0.0 to 192.168.255.255, giving you 254 possible subnetworks, each with 254 possible hosts. The number 127.0.0.0 is reserved for a system's loopback interface, which allows it to communicate with itself, as it enables users on the same system to send messages to each other.

These numbers were originally designed for class-based addressing. However, they can just as easily be used for Classless Interdomain Routing (CIDR) addressing, where you can create subnetworks with a smaller number of hosts. For example, the 254 hosts addressed in a class C network could be split into two subnetworks, each with 125 hosts. See Chapter 35 for more details.

### IPv6 Private Networks

IPv6 supports private networks with site-local addresses that provide the same functionality of IPv4 private addresses. The site-local addresses have no public routing information. They cannot access the Internet. They are restricted to the site they are used on. The site-local addresses use only three fields: a format prefix, subnet identifier, and interface identifier.

| Address | Networks |
| :--- | :--- |
| 10.0.0.0 | Class A network |
| 172.16.0.0–172.31.255.255 | Class B network |
| 192.168.0.0 | Class C network |
| 127.0.0.0 | Loopback network (for system self-communication) |

**TABLE 36-1** Non-Internet Private Network IP Addresses

A site-level address has the format prefix **fec0**. If you have no subnets, it will be set to 0. This will give you a network prefix of **fec0:0:0:0**. You can drop the set of empty zeros to give you **fec0:**. The interface ID field will hold the interface identification information, similar to the host ID information in IPv4.

```
fec0::    IPv6 site-local prefix
```

The loopback device will have special address of ::1, also known as localhost.

```
::1       IPv6 loopback network
```

Rather than using a special set of reserved addresses as IPv4 does, with IPv6 you only use the site-local prefix, **fec0**, and the special loopback address, ::1.

> **Tip** Once your network is set up, you can use *ping6* or *ping* to see if it is working. The *ping6* tool is designed for *IPv6* addresses, whereas *ping* is used for *IPv4*.

## Local Network Address Example Using IPv4

If you are setting up a LAN, such as a small business or home network, you are free to use class C IPv4 network (254 hosts or less) that have the special network number 192.168, as used in these examples. These are numbers for your local machines. You can set up a private network, such as an intranet, using network cards such as Ethernet cards and Ethernet hubs, and then configure your machines with IP addresses starting from 192.168.0.1. The host segment can range from 1 to 254, where 255 is used for the broadcast address. If you have three machines on your home network, you can give them the addresses 192.168.0.1, 192.168.0.2, and 192.168.0.3. You can then set up domain name services for your network by running a DNS server on one of the machines. This machine becomes your network's DNS server. You can then give your machines fully qualified domain names and configure your DNS server to translate the names to their corresponding IP addresses. As shown in Figure 36-2, for example,

![](img/ab68ea377332b50bf70ef1316c8175b6_866_0.png)

you could give the machine 192.168.0.1 the name **turtle.mytrek.com** and the machine 192.168.0.2 the name **rabbit.mytrek.com**. You can also implement Internet services on your network such as FTP, Web, and mail services by setting up servers for them on your machines. You can then configure your DNS server to let users access those services using fully qualified domain names. For example, for the **mytrek.com** network, the Web server could be accessed using the name **www.mytrek.com**. Instead of a Domain Name Service, you could have the */etc/hosts* files in each machine contain the entire list of IP addresses and domain names for all the machines in your network. But for any changes, you would have to update each machine's */etc/hosts* file.

## BIND

The DNS server software currently in use on Linux systems is Berkeley Internet Name Domain (BIND). BIND was originally developed at the University of California, Berkeley, and is currently maintained and supported by the Internet Software Consortium (ISC). You can obtain BIND information and current software releases from its Web site at **www.isc.org**. Web page documentation and manuals are included with the software package. At the site you can also access the BIND Administration Manual for detailed configuration information. RPM packages are available at distribution FTP sites. The BIND directory in */usr/share/doc* contains extensive documentation, including Web page manuals and examples. The Linux HOW-TO for the Domain Name System, DNS-HOWTO, provides detailed examples. Documentation, news, and DNS tools can be obtained from the DNS Resource Directory (DNSRD) at **www.dns.net/dnsrd**. The site includes extensive links and online documentation, including the *BIND Operations Guide* (BOG). See Table 36-2 for a list of DNS resources.

### Alternative DNS Servers

Several alternative DNS servers are now available. These include djbdns, noted for its security features, CustomDNS, a dynamic server implemented in Java (**custodns.sourceforge.net**), and Yaku-NS, an embedded server. The djbdns server (**cr.yp.to/djbdns.html**), written by D.J. Bernstein, is designed specifically with security in mind, providing a set of small server daemons, each performing specialized tasks. In particular, djbdns separates the name server, caching server, and zone transfer tasks into separate programs: tinydns (**tinydns.org**) implements the authoritative name server for a network, whereas dnscache implements a caching server that will resolve requests from DNS clients such as Web browsers. In effect, dnscache operates as the name server that your applications will use to resolve addresses. dnscache will then query tinydns to resolve addresses on your local network. Zone transfers are handled separately by axfrdns and asget.

| Web Site | Resource |
| :--------- | :--------- |
| **www.isc.org** | Internet Software Consortium |
| **www.dns.net/dnsrd** | DNS Resource Directory |
| **www.nomimum.com** | Nominum, BIND support and consulting |

**TABLE 36-2** BIND Resources
