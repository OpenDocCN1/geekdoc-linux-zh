| Prefix | Hosts |
| :--- | :--- |
| /19 | 8,192 hosts |
| /20 | 4,096 hosts |
| /21 | 2,048 hosts |
| /22 | 1,024 hosts |
| /23 | 512 hosts |
| /24 | 256 hosts |
| /25 | 128 hosts |
| /26 | 64 hosts |
| /27 | 32 hosts |

The CIDR addressing scheme also helps reduce the routing overload problem by having a single, high-level route represent many lower-level routes. For example, an ISP could be assigned a single /13 IP network and assign the 500,000-plus addresses to its customers. Routers outside the ISP would only need to know how to reach the ISP for those half-million addresses. The ISP would then be responsible for maintaining routing information for all of the host routes with that network address.

# ## Getting IP addresses

So, what is the impact of assigning IP addresses to the computers on your LAN? Your choice of which IP addresses to use depends on your situation. If you are part of a large organization, you should get addresses from your network administrator. Even if you don't connect to other LANs in your organization at the moment, having unique addresses can make it easier to connect to them in the future.

If you are setting up a network for yourself (with no other networks to consider in your organization), you can use private addresses. However, if you need to connect computers to the Internet as servers, apply for your own domain name (from an Internet domain registrar) and IP addresses (from your ISP).

> **CROSS-REFERENCE:** Refer to Chapter 25 for information about getting the IP addresses and domain names you need to configure a public server on the Internet.

If you don't need to have your LAN accessible from the Internet, choose IP addresses from the set of available general-purpose IP addresses. Using these private IP addresses, you can still access the Internet from your LAN for such things as Web browsing and e-mail by using IP masquerading or Network Address Translation (NAT), as described in Chapter 16. Table 15-3 lists the private IP addresses not used on any public part of the Internet.

# **Table 15-3: Private IP Addresses**

| Network Class | Network Numbers | Addresses per Network Number |
| :--- | :--- | :--- |
| Class A | 10.0.0.0 | 167,777,216 |
| Class B | 172.16.0.0 to 172.31.0.0 | 65,536 |
| Class C | 192.168.0.0 to 192.168.255.255 | 256 |