
interconnecting servers that manage the Domain Name System (also referred to as DNS servers or name servers). These DNS servers keep lists of fully qualified domain names and their IP addresses, matching one up with the other. This service that they provide to a network is referred to as the Domain Name System. The Internet is composed of many connected subnets called domains, each with its own Domain Name System (DNS) servers that keep track of all the fully qualified domain names and IP addresses for all the computers on its network. DNS servers are hierarchically linked to root servers, which, in turn, connect to other root servers and the DNS servers on their subnets throughout the Internet. The section of a network for which a given DNS server is responsible is called a zone. Although a zone may correspond to a domain, many zones may, in fact, be within a domain, each with its own name server. This is true for large domains where too many systems exist for one name server to manage.

## DNS Operation

When a user enters a fully qualified domain name to access a remote host, a resolver program queries the local network’s DNS server requesting the corresponding IP address for that remote host. With the IP address, the user can then access the remote host. In Figure 34-1, the user at rabbit.mytrek.com wants to connect to the remote host lizard.mytrek.com. rabbit.mytrek.com first sends a request to the network’s DNS server—in this case, turtle.mytrek.com—to look up the name lizard.mytrek.com and find its IP address. It then returns the IP address for lizard.mytrek.com, 192.168.0.3, to the requesting host, rabbit.mytrek.com. With the IP address, the user at rabbit.mytrek.com can then connect to lizard.mytrek.com.

![](img/6c226e8ba1efd427dec3bf582418d33f_688_0.png)

## DNS Clients: Resolvers

The names of the DNS servers that service a host’s network are kept in the host’s /etc/resolv.conf file (see Chapter 38). When setting up an Internet connection, the name servers provided by your Internet service provider (ISP) were placed in this file. These name servers resolve any fully qualified domain names that you use when you access different Internet sites. For example, when you enter a Web site name in your browser, the name is looked up by the name servers and the name’s associated IP address is then used to access the site.

```
/etc/resolv.conf
search mytrek.com mytrain.com
nameserver 192.168.0.1
nameserver 192.168.0.3
```

## Local Area Network Addressing

If you are setting up a DNS server for a local area network (LAN) that is not connected to the Internet, you should use a special set of IP numbers reserved for such local networks (also known as private networks or intranets). This is especially true if you are implementing IP masquerading, where only a gateway machine has an Internet address, and the others make use of that one address to connect to the Internet. For a class C IPv4 network (254 hosts or less), these are numbers that have the special network number 192.168, as used in these examples. If you are setting up a LAN, such as a small business or home network, you are free to use these numbers for your local machines. You can set up a private network, such as an intranet, using network cards such as Ethernet cards and Ethernet hubs, and then configure your machines with IP addresses starting from 192.168.0.1. The host segment can range from 1 to 254, where 255 is used for the broadcast address. If you have three machines on your home network, you can give them the addresses 192.168.0.1, 192.168.0.2, and 192.168.0.3. You can then set up domain name services for your network by running a DNS server on one of the machines. This machine becomes your network’s DNS server. You can then give your machines fully qualified domain names and configure your DNS server to translate the names to their corresponding IP addresses. As shown in Figure 34-2, for example, you could give the machine 192.168.0.1 the name turtle.mytrek.com, and the machine 192.168.0.2 the name rabbit.mytrek.com. You can also implement Internet services on your network such as FTP, Web, and mail services by setting up servers for them on your machines. You can then configure your DNS server to let users access those services using fully qualified domain names. For example, for the mytrek.com network, the Web server could be accessed using the name www.mytrek.com. Instead of a Domain Name Service, you could have the /etc/hosts files in each machine contain the entire list of IP addresses and domain names for all the machines in your network. But for any changes, you would have to update each machine’s /etc/hosts file.

## IPv4 Private Networks

IPv4 provides a range of private addresses for the three classes supported by IPv4. As you have seen, class C IPv4 network numbers that have the special network number 192.168.
