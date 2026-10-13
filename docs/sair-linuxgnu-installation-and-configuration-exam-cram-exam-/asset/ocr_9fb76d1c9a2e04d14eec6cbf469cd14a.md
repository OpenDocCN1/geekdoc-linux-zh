Table 12.3 Example network addresses and network masks.

| Network Address | Network Mask | Host Address Range | Number of Usable IP Addresses |
|---|---|---|---|
| 10.0.0.0 | 255.0.0.0 | 10.0.0.1-10.255.255.254 | 16,777,214 |
| 10.53.0.0 | 255.255.0.0 | 10.53.0.1-10.53.255.254 | 65,534 |
| 10.126.13.0 | 255.255.255.0 | 10.126.13.1-10.126.13.254 | 254 |
| 172.168.0.0 | 255.255.0.0 | 172.168.0.1-172.168.255.254 | 65,534 |
| 172.168.156.0 | 255.255.255.0 | 172.168.156.1-172.168.156.254 | 254 |
| 192.168.0.0 | 255.255.255.0 | 192.168.0.1-192.168.0.254 | 254 |

From Table 12.3, you can derive the following "rules" for IP addressing:

+   - A network IP address is never used for a specific computer. This address precedes the host address range.
+   - The 255s in a network mask correspond to the network address. For example, if your IP address is 10.162.4.23 and your network mask is 255.255.255.0, the network address is 10.162.4.0. The "host" part of the IP address is 23.
+   - The last address in an IP address range is never used. For example, from the last network shown in Table 12.3, the last address is 192.168.0.255, which is reserved for the broadcast address.
+   - For Class A addresses, you can have a network mask of 255.0.0.0, 255.255.0.0, or 255.255.255.0. For Class B addresses, you can have a network mask of 255.255.0.0 or 255.255.255.0. For Class C addresses, you can have a network mask of 255.255.255.0. Although there are other network masks available, understanding all masks is not important to this chapter.

![](bbox=[0.13, 0.82, 0.22, 0.92])

> Be able to use a network mask to break down an IP address into a network address and a host address.

# Setting Up a Network

Before you set up a TCP/IP network, you need to select a set of addresses. Based on the previous sections, you can choose a network address and network mask. When you put the two together, you get a range of IP addresses that you can assign within a LAN.

Perhaps the most common network mask is 255.255.255.0. As discussed earlier, this network mask allows you to choose from 254 IP addresses. In other