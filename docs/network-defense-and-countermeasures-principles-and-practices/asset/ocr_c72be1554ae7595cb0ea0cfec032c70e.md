# The Basics of a Network

Subnetting also allows you to use certain, limited subsets. Another approach is CIDR, or classless interdomain routing. Rather than define a subnet mask, you have the IP address followed by a slash and a number. That can be any number between 0 and 32, which results in IP addresses like these:

192.168.1.10/24 (basically a Class C IP address)

192.168.1.10/31 (like a Class C IP address with a subnet mask)

When you use this, rather than having classes with subsets, you have variable-length subnet masking (VLSM) that provides classless IP addresses. This is the most common way to define IP addresses today.

You should not be concerned that new IP addresses are likely to run out. The IPv6 6 standard is already available, and methods are in place to extend the use of IPv4 addresses. The IP addresses come in two groups: public and private. The public IP addresses are for computers connected to the Internet. No two IP addresses can be the same. However, a private IP address, such as one on a private company network, has to be unique in that network. It does not matter if computers in the world have the same IP address, because this computer is never connected to other worldwide computers. Network administrators often use private IP addresses that begin with a 10, such as 10.0.102.230. The other private IP addresses are 172.16.0.0-172.31.255.255 and 192.168.0.0-192.168.255.255.

Also note that an ISP will pull a pool of IP addresses and assign them to when you log on. So, an ISP may might its own pool of IP addresses and have 10,000 customers. Because all 10,000 customers will not be at the same time, the ISP simply assigns an IP address to a customer when she or he logs on, and the ISP unassigns the IP address when the customer logs off.

IPv6 utilizes a 128-bit address (instead of 32) and utilizes a hex numbering method in order to avoid long addresses such as 132.64.34.64.156.143.57.1.3.7.44.122.111.201.5. The hex address appears in the form of FFFE:800::example. This gives you 2¹⁸ possible addresses (many trillions of addresses), so no chance of running out of IP addresses in the foreseeable future.

There is no subnet in IPv6. Instead, it uses CIDR. The network portion is indicated by a slash followed by the number of bits in the address that are assigned to the network portion, as such

```
/48
```

```
/64
```

There is a loopback address for IPv6, and it is written as ::128. Other differences between IPv4 and IPv6 are described here:

+   - Link/machine-local.

+   - IPv6 version of IPv4's APIPA or Automatic Private IP Addressing. So if the machine is configured for dynamically assigned addresses and cannot communicate with a DHCP server, it assigns itself a generic IP address. DHCP, or Dynamic Host Configuration Protocol, is used to dynamically assign IP addresses within a network.