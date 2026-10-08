# 4.2.1 IP Addressing and Subnetting

As you already know, but I feel compelled to write, IP addresses for version 4 of IP consist of four 32-bit numbers separated by periods, known as the "dotted quad" or "dotted decimal" notation. Although seemingly everyone understands or at least seen an IP address, it certainly seems as though fewer and fewer understand subnetting and the subnet masks that are an important part of the IP addressing scheme. This section briefly looks at addressing and subnetting.

IP addresses are divided into different classes rather than being an entirely flat space. The classes for IP addresses are shown in Table 4.1.

Table 4.1 Internet Range

| Class | Address Range |
|---|---|
| A | 0.0.0.0 to 127.255.255.255 |
| B | 128.0.0.0 to 191.255.255.255 |
| C | 192.0.0.0 to 223.255.255.255 |
| D | 224.0.0.0 to 239.255.255.255 |
| E and unallocated | 240.0.0.0 to 255.255.255.255 |

In practice, addresses in Classes A through C are for general Internet use. However, some readers may have experience with Class D addresses, frequently used for multicast. Class E is the experimental and unallocated range.

# SPECIAL IP ADDRESSES

There are three major special cases of IP addresses:

+   * Network address 0—As noted under Class A addresses, network address 0 is not used as part of a routable address. When used as a source address, its only legal use is during initialization when a host is attempting to have its IP address dynamically assigned by a server. When used as a destination, only address 0.0.0.0 means, and then only to the local machine as referring to it, or as a connection to refer to a default route.
* Loopback network address 127—As noted under Class A addresses, network address 127 is not used as part of a routable address. Loopback addresses refer to a private network interface supported by the operating system. The interface is used as the addressing mechanism for local network-based services. In other words, local network clients use it to address local servers. Loopback traffic remains entirely within the operating system. It is never passed to a physical network interface. Typically, 127.0.0.1 is the only loopback address used, referring to the local host.