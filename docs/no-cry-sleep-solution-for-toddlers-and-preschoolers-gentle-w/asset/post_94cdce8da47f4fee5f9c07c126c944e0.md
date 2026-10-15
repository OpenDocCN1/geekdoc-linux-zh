
## Network Administration

## PART

- CHAPTER 34
  Domain Name System
- CHAPTER 35
  DHCP Server
- CHAPTER 36
  NFS and NIS
- CHAPTER 37
  Samba
- CHAPTER 38
  Administering TCP/IP Networks

## CHAPTER
Domain Name System

The Domain Name System (DNS) is an Internet service that locates and translates domain names into their corresponding Internet Protocol (IP) addresses. As you may recall, all computers connected to the Internet are addressed using an IP address. As a normal user on a network might have to access many different hosts, keeping track of the IP addresses needed quickly became a problem. It was much easier to label hosts with names and use the names to access them. Names were associated with IP addresses. When a user used a name to access a host, the corresponding IP address was looked up first and then used to provide access.

### DNS Address Translations

The process of translating IP addresses into associated names is fairly straightforward. Small networks can be set up easily with just the basic configuration. The task becomes much more complex with larger networks and the Internet. The sheer size of the task can make DNS configuration a complex operation.

### Fully Qualified Domain Names

IP addresses were associated with corresponding names, called fully qualified domain names. A fully qualified domain name is composed of three or more segments. The first segment is the name that identifies the host, and the remaining segments are for the network in which the host is located. The network segments of a fully qualified domain name are usually referred to simply as the domain name, while the host part is referred to as the hostname (though this is also used to refer to the complete fully qualified domain name). In effect, subnets are referred to as domains. The fully qualified domain name www.linux.org could have an IP address 198.182.196.56, where 198.182.196 is the network address and 56 is the host ID. Computers can be accessed only with an IP address, so a fully qualified domain name must first be translated into its corresponding IP address to be of any use. The parts of the IP address that make up the domain name and the hosts can vary. See Chapter 38 for a detailed discussion of IP addresses, including network classes and Classless Interdomain Routing (CIDR).

### IPv4 Addresses

The IP address may be implemented in either the newer IPv6 (Internet Protocol Version 6) format or the older and more common IPv4 (Internet Protocol Version 4) format. Since the IPv4 addressing is much easier to read, that format will be used in these examples. In the older IPv4 format, the IP address consists of a number composed of four segments separated by periods. Depending on the type of network, several of the first segments are used for the network address and one or more of the last segments are used for the host address. In a standard class C network used in smaller networks, the first three segments are the computer’s network address and the last segment is the computer’s host ID (as used in these examples). For example, in the address 192.168.0.2, 192.168.0 is the network address and 2 is the computer’s host ID within that network. Together, they make up an IP address by which the computer can be addressed from anywhere on the Internet. IP addresses, though, are difficult to remember and easy to get wrong.

### IPv6 Addressing

IPv6 addressing uses a very different approach designed to provide more flexibility and support for very large address spaces (see Chapter 38). There are three different types of IPv6 addresses, unicast, multicast, and anycast, of which unicast is the most commonly used. A unicast address is directed to a particular interface. There are several kinds of unicast addresses, depending on how the address is used. For example, you can have a global unicast address for access through the Internet or a site-level unicast address for private networks.

Although consisting of 128 bits in eight segments (16 bits, 2 bytes per segment), an IPv6 address is made up of several fields that conform roughly to the segments and capabilities of an IPv4 address, networking information, subnet information, and the interface identifier (host ID). The network information includes a format prefix indicating the type of network connection. In addition, a subnet identifier can be used to specify the local subnet (see Chapter 38). The network information takes up the first several segments. The remainder is used for the interface ID. The interface ID is a 64-bit (four segments) Extended Unique Identifier (EUI-64) generated from a network device’s Media Access Control (MAC) address. IP addresses are written in hexadecimal numbers, making them difficult to use. Each segment is separated by a colon, and a set of consecutive segments with zero values can be left empty.

### Manual Translations: /etc/hosts

Any computer on the Internet can maintain a file that manually associates IP addresses with domain names. On Linux and Unix systems, this file is called the /etc/hosts file. Here, you can enter the IP addresses and domain names of computers you commonly access. Using this method, however, each computer needs a complete listing of all other computers on the Internet, and that listing must be updated constantly. Early on, this became clearly impractical for the Internet, though it is still feasible for small isolated networks.

### DNS Servers

The Domain Name System has been implemented to deal with the task of translating the domain name of any computer on the Internet to its IP address. The task is carried out by
