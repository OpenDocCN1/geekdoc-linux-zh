
# IP Addresses

Every device that is fully connected to the Internet is called a **host**, and each such device must have a unique Internet address (also called an **IP address**). An IP address is a four-byte number, called a *dotted quad*, written using decimal equivalents, with each number separated by a dot, such as 192.168.100.44.

Each IP address begins with a portion that is *shared by all the hosts* within a network; this section is called the *network portion*. The remaining portion of the IP address identifies unique hosts within the network. This portion is called the *host portion*.

# Address Classes

Internet addresses are divided into *classes* for administrative purposes. **Class A** networks have IP addresses that begin with a number that is less than 128. **Class B** networks have IP addresses that begin with 128 through 191. **Class C** networks have IP addresses that begin with 192 through 223. These networks vary in the number of hosts that they can accommodate. For example, class A networks can have millions of hosts, while class B networks can have a maximum of 65,534 hosts, and class C networks are limited to 254 hosts.

Some IP addresses are reserved for special uses. In all network classes, host number 0 is reserved for the *network address*, while host number 255 is reserved for the *broadcast address*. In addition, the following addresses are reserved:

- 127.0.0.1 This address, called the *loopback address*, is reserved so that a host can address itself.
- 10.0.0.0 This network address is reserved for private, internal networks that can accommodate millions of hosts.
- 172.16.0.0 This network address is reserved for private, internal networks that can accommodate thousands of hosts.
- 192.168.0.0 This network address is reserved for private, internal networks that can accommodate up to 254 hosts.

## Netmasks and Network Addresses

Where does the network portion end, and where does the host portion begin? To determine this, you need to know the *netmask*. The netmask is another four-byte number; like an IP address, it is written with four decimal numbers, separated by dots. However, the netmask can contain only two numbers: 0 and 255. The number 255 is used to specify those portions of the address that make up the network portion, while the 0 is used to specify the portions of the address that make up the host portion. If the netmask is 255.255.255.0 and the IP address is 192.168.100.44, the network portion is 192.168.100, while the host portion is the last of the four numbers in the address. Additionally, the *network address* is the lowest possible address available for a host in the network. In the previous example, the network address is 192.168.100.0.

## Broadcast Address

In addition to the addresses already mentioned, a given network has a *broadcast address*. This is the address that is monitored by every workstation on the network. By convention, the broadcast address is typically the network address with a final decimal value of 255. For the network with an address of 192.168.100.0, the broadcast address is 192.168.100.255.

## Gateway Address

If your computer is connected to a local area network with access to the external Internet, or to another private network, you will need to know about yet another type of IP address: the *gateway address*. The gateway address is the IP address of the device that provides access to external networks. For example, suppose your local area network is connected to an ISDN adapter and router, which enables all the computers on your network to access the external Internet. The IP address of this device is 192.168.100.7. This is the *Gateway address* for your network. To access the external Internet, you will need to configure each machine on the network so that it knows the gateway address. See the section “/etc/sysconfig/network” for more information about configuring Linux systems to use a gateway address.

# Domain Name Service (DNS) and Domain Names

As the previous section explained, every host connected to a TCP/IP network has its own, unique IP address. However, IP addresses are difficult for people to work with. Moreover, a given machine's address may change if it is connected to a different network. The *Domain name service (DNS)* solves this problem by mapping people-friendly *domain names*, such as *www.yahoo.com*, to specific IP addresses.

The *domain name service* is a worldwide service that involves the use of servers at many levels. However, the DNS server of greatest importance to you is the default DNS server for your network. If you connect to the Internet by means of a dial-up (modem) connection, you need to know the IP address of your Internet service provider's DNS server. If you are connecting to a private, internal network, you need to know the IP address of the computer that is running the DNS service locally.

# Network Interfaces

To connect your Linux system to a TCP/IP network, you need to assign IP addresses to *network interfaces*. In brief, a network interface is a device, such as an Ethernet card or modem, that enables your computer to connect to a TCP/IP network. In Linux, network interfaces are created by the modules that support the device in question. For example, when *modprobe* detects an Ethernet card, it assigns the network interface *eth0* to the first detected card, *eth1* to the second detected card, and so on. Similarly, if you connect to the Internet by means of a modem running the PPP protocol, the software that supports your modem assigns the network interface *ppp0* to the first detected modem, *ppp1* to the second, and so on.

Although the software that supports networking peripherals assigns network interfaces automatically, you still need to associate each network interface with an IP address. Addresses can be assigned in two ways, *statically* or *dynamically*. In static addressing, you type the IP address that the network interface will use. In dynamic addressing, the IP address is automatically determined by services such as bootp or dhcp. If you plan to connect your Linux system to a local area network (LAN), ask the network administrator what type of address to use. If you are connecting to an Internet service provider using the PPP protocol, you will probably use dynamic addressing.

# Network Services and Ports

TCP/IP uses a client/server design, in which network applications require two different types of programs. Users make use of a client program to obtain data of a particular type, such as FTP (for files located on the network), Web pages, or e-mail. Servers make a certain type of information available to clients. Although it’s quite possible to run clients and servers on the same machine, the more usual arrangement is that users run clients on their machines and obtain data from the network by contacting servers running on other machines. Generally provided by means of a daemon running in the background, server software provides a distinctive type of TCP/IP service. If you are running FTP, Web, and mail servers, these three services are available from your computer.

So that TCP/IP can route incoming and outgoing signals to the various services correctly, TCP/IP associates a given type of networking service with a well-known port, a number that stands for a virtual electronic interface. For example, FTP is associated with port 21, while the Web servers are associated with port 80. The file called /etc/services lists all the ports that are defined for use on your system.

# Disabling Unneeded Servers

Because Linux comes with a variety of powerful, built-in servers, it is deservedly popular among organizations looking for low-cost server solutions. However, most of the readers of this book have no need to run server software. Nevertheless, Linux distributions may install and enable a variety of servers, and these may be running without the user being aware of this fact. Poorly configured or out-of-date servers could present potential intruders with a means of gaining unauthorized access to a Linux system. For this reason, it is a good practice to determine which TCP/IP servers are running on your system. Furthermore, you should disable any services that you do not need.
