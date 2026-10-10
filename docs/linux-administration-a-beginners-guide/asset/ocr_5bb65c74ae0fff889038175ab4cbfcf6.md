**NOTE:** An octet is 8 bits, which in the typical dotted-decimal notation of IP means the first set of numbers. For example, in the IP address 192.168.1.42, the first octet is 192.

The ranges are as follows:

| Class | Octet Range |
| :--- | :--- |
| A | 0–126 (except 10) |
| B | 128–192.167 (except 172) |
| C | 192.169–223 |

**NOTE:** There are also class D and class E ranges. Class D is used for multicast, and class E is reserved for experimental usage.

You probably noticed some gaps in the ranges. This is because there are some special addresses that are reserved for special uses. The first special address is one you are likely to be familiar with: **127.0.0.1**. This is also known as the loopback address. It is set up on every host using IP so that it can refer to itself. It seems a bit odd to do it this way, but just because a system is capable of speaking IP doesn't mean it has an IP address allocated to it! On the other hand, the 127.0.0.1 address is virtually guaranteed. (If it isn't there, more likely than not, something has gone wrong.)

Three other ranges are notable: every IP in the **10.0.0.0** network, the **172.16** through **172.31** networks, and the **192.168** network are considered *private* IPs. These ranges are not allowed to be allocated to anyone on the Internet, and therefore, you may use them on your internal networks.

**NOTE:** We define *internal networks* as networks that are behind a firewall, not really connected to the Internet, or have a router performing network address translation for it at the edge of the network connecting to the Internet. (Most firewalls perform this address translation as well.)

# Subnetting

Imagine a network with a few thousand hosts on it. (Not unreasonable on a medium-sized company.) Trying to fit them all together into a single large network would probably lead you to pull out all your hair, beat your head into a wall, or possibly both. And that's just the figurative stuff.