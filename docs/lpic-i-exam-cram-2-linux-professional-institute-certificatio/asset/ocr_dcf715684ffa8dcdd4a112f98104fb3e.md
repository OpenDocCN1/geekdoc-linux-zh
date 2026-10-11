section and a host section. The network mask sets where network bits end and host-assignable bits begin.

For each class, the point at which a network mask stops is where the network portion of an address ends and the host-assignable portion begins. For example, if you take the address 192.168.1.200 and a default subnet mask, the first three octets represent the network and the last octet is where hosts can be assigned.

Address class ranges come with their own built-in default subnet mask; only one can be the default per range:

+   - **A**—255.0.0.0 or /8 for the number of bits that represent the network mask
+   - **B**—255.255.0.0 or /16 for the number of bits that represent the network mask
+   - **C**—255.255.255.0 or /24 for the number of bits that represent the network mask

![](bbox=[0.1, 0.49, 0.16, 0.56])

> LPI follows the industry in its use of either fully spelled-out network masks (255.255.255.0) or using abbreviated notation (/24) to represent any network mask assigned to a host or set of hosts. The number 24 relates to the number of bits used for the subnet mask. 
> 
> Be prepared to solve questions that use either method of expressing the network mask.

# ## Using Default Network Masks

As previously mentioned, the place where the network portion of an address ends is where the subnet mask bits stop. If you have a network address such as 192.168.10.0 and a default subnet mask of 255.255.255.0 or /24, a single network (192.168.10.0) exists and the remaining 8 bits that are outside the network portion are available for assignment to hosts.

It might help to express the network address and then the network mask as a set of bits, like so:

```
```
11000000 . 10101000 . 00001010 . 00000010   (The IP)
11111111 . 11111111 . 11111111 . 00000000   (The Subnet Mask)
```
```

Because the network mask is a /24, or default Class C network mask, you can easily see where the network begins and ends and what’s usable for host addresses. The boundary in this example is the last dot, leaving 8 bits worth of addresses for this single network assignable to hosts.