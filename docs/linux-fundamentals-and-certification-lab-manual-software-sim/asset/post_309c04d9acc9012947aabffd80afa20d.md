
![](img/37f079cee226b270f2e09b37a2e4a05d_183_0.png)

IP addresses are divided into five classes. Three of these can be used for hosts on a network, classes A, B, or C. Two classes are reserved. Class D addresses are reserved for multicast and class E addresses are reserved for experimental use.

Class A addresses, when written in binary format, always start with a 0. In a class A network, the leftmost octet is used for network identification, and the right three octets are used to identify hosts. The range of class A addresses in the first octet is 0–126. (127 is reserved for localhost specification.) The number of hosts that are available on a class A network is $2^{24}$ minus 2, or 16,777,214.

> **NOTE**
>
> You raise 2 to the 24th power because the host takes the last three octets (3 · 8). The reason for subtracting 2 is that in the host portion, all zeros is used for network identification and all ones is used for broadcast.

A broadcast occurs when a source host sends out data to all hosts on a network. The address that identifies that the message is a broadcast message always has all ones in the host positions. The network 192.168.0.0 has a broadcast of 192.168.0.255 (all ones in the host position, 1111 1111).

Class B addresses, when written in binary format, always start with 10 in the first two bits. In a class B network, the first two octets are used for network identification and the last two octets for host identification. The range of values in the first octet of a class B network is 128–191. The number of hosts available on a class B network is $2^{16}$ minus 2, or 65,534.

Class C addresses when written are always 110 in the first three binary positions. In a class C network, the first three octets are used to identify the network and the last octet identifies the hosts. The range of a class C address in the first octet is 192–223. The number of hosts available on a class C network is $2^8$ minus 2, or 254.

It is important to understand why an IP address has a network and a host portion. A host can directly communicate only with other hosts on the same network. If the hosts have a different network ID they cannot communicate directly with each other without a router between the two.

The number of network bits is fixed, depending on the class of the network. The network bits are identified by a subnet mask. The subnet mask is 32 bits, corresponding with the associated IP address. The subnet mask bits have a value of 1 for any network positions and a value of 0 for any host positions. For example, a host with the address 192.168.0.1 will have a subnet mask of 255.255.255.0 (Figure 7–9). (All ones, 1111 1111, has a decimal equivalent of 255.)

![](img/37f079cee226b270f2e09b37a2e4a05d_183_1.png)

This indicates that the network is 192.168.0 and the host is 1.

Sometimes it is appropriate to divide the host bits among logical groups. As stated earlier in this chapter, hosts in a network can communicate directly only with other hosts in the same network. For example, if the users of the host machines that deal with payroll were in a separate network, users on a host outside the network would not be able to connect to the payroll resources. This would increase security on the overall network.

For example, if you have a class C address, giving you 254 possible hosts, you may prefer to place them logically by department instead of grouping all users together. Assume the following:

- Class C address of 192.168.0.0
- 10 users are in inventory control
- 8 users are in accounts payable
- 8 users are in accounts receivable
- 5 users are in payroll
- 5 users are in management

By default you have one network, 192.168.0.0, and 254 hosts (host bits 0–255, using 0 for the network address and 255 for broadcast). TCP/IP addressing allows the use of some host bits for the network. The bits borrowed from the host bits that are for network use are called subnet bits. To be useful, you must leave at least two bits for host use. (Allowing for all zeros for network ID and all ones for broadcast leaves two addresses for hosts.)

Before you borrow host bits for subnet bits, determine how many subnets you need. From the above information, you need to divide the users of hosts to obtain a minimum of five groups or subnets. Remember that the network bits have a value of 1 in the subnet mask. With subnets, you have a range of networks, with the 1 in the subnet indicating which network you are using. (The default network bits in the subnet mask always have a value of one.)

All you have to do is count the subnet bits you need, adding the values to determine the networks that will be available. Figure 7-10 counts the subnet bits needed.

### FIGURE 7-10
Counting subnet bits.

**Counting Subnet Bits**

| Decimal | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **32** | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 |
| **64** | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 |
| **96** | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 0 |
| **128** | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| **160** | 1 | 0 | 1 | 0 | 0 | 0 | 0 | 0 |
| **192** | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 |
| **224** | 1 | 1 | 1 | 0 | 0 | 0 | 0 | 0 |

The first subnet is 192.168.0.0, which would mean all zeros in the host bit portion and used for network ID. The usable subnets would be:

- 192.168.0.32
- 192.168.0.64
- 192.168.0.96
- 192.168.0.128
- 192.168.0.160
- 192.168.0.192

The last subnet, 192.168.0.224, would be all ones and used for broadcast.

The subnet mask for this group of subnets would be 255.255.255.224, indicating that three bits would be borrowed from the host bits. Discounting all ones and all zeros, each subnet would accommodate up to 30 host machines.

## Other Addresses

Before you can get off a single subnet, you have to have a way to route the packets to a remote network. As previously discussed, a router is the device used to connect networks. To complete the network setup you must have a few more addresses.

To connect to a router, the interface on the router must have a network address compatible with the network your hosts are on. If you are using network 192.168.0.0, your usable hosts range is from 192.168.0.1 to 192.168.0.254. The router can use any of the available addresses. Whatever the router interface address, that is the address of the network *gateway*.

Even if you can route with the router, you still have to know where to connect. A DNS server takes the requested URL and returns the IP address of the host that owns it.

## BASIC NETWORK CONFIGURATION

Using a network with Linux allows you to access the Internet, connect to remote machines, provide network services for other machines, and more. Before configuring a network you need to understand something about client/server relationships.

## Client/Server

Computers have many different purposes. Some computers are used for stand-alone personal productivity applications, such as word processing or maintaining a simple checkbook, whereas others are used to provide services to other computers. The term “client/server” just refers to the role of individual computers on a network. A machine that provides services to other computers is called a server, and a machine that uses services provided by a server is called a client. A computer can be both a client and a server.

For example, if you connect to the Internet and browse Web pages, you are a client. When you connect to a site, www.inuxiso.org for example, your computer requests an IP address for the remote machine. A DNS server responds with the IP address, and then your machine connects to the remote IP address. With a Web browser application, your machine requests a document (Web page), which a Web server provides. If your computer is providing disk space for another user on your network, your computer is a file server.

To use your computer as a client or a server, it must be configured to connect to the network. The first step in configuring the network is to set the Ethernet card for the correct parameters.

## Ethernet Configuration

The network setup on a computer can be configured two different ways—statically and dynamically. A static configuration requires that you set the IP address, subnet mask, gateway, and DNS servers. Static configuration is a good idea for servers. A dynamic configuration sets up the IP address, subnet mask, gateway, and DNS servers from a DHCP server. The DHCP client broadcasts a message, announcing that it is connected and needs an IP address to connect to the network. The server then responds with the needed information.

## DHCP Configuration

Dynamic Host Configuration Protocol (DHCP) is part of the TCP/IP suite of protocols and is backward compatible with BOOTstrap protocol (BOOTP). DHCP servers provide an IP address from an address pool. The values are defined and automatically assigned as clients request them. With DHCP the entire network configuration can be retrieved from the DHCP server, including IP address, subnet mask, gateway, DNS servers, and other settings.
