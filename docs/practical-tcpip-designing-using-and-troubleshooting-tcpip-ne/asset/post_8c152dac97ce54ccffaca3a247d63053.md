
## 4.2 The historical IP address classes

TCP/IP routing views any IP address as two parts – *a network part* and *a host part*:

- the network part of the address identifies the network the machine is connected to
- the rest of the address – the host part – identifies the particular machine on that network.

Routing on your machine uses the network part to decide whether the destination machine is on the same network as your own. If the network part of the destination address is the same as the network part of your own address, then the two machines are locally connected; otherwise they’re not.

Historically, TCP/IP used *address classes* to decide how to extract the host and network parts. Addresses are divided into five classes, A, B, C, D, and E.

- D is used for multicasting (see Module 4.11)
- E is reserved and not yet used
- A, B, and C, which are all we are concerned with here, are used for normal addresses.

The class an IP address belongs to is determined by its top few bits, as shown in Figure 4.2. Just by looking at these bits TCP/IP can tell immediately from an address which class it belongs to, so class-based routing decisions can be processed quickly in the routing code.

![](img/a2132b646d336d5f9a21102d6320e537_117_0.png)

**Figure 4.2** The IP address classes

Because a specific number of bytes or bits is used for network/host parts in each class, it follows automatically how many networks of each type there are, and how big each of them is (Table 4.1).

**Table 4.1** Network types and sizes

|   | Address range | Network part | Number of networks | Host part | No. hosts per network |
|---|---|---|---|---|---|
| A | 0.0.0.0–127.255.255.255 | 1 + 7 bits | 128 | 24 bits | 16,777,216 |
| B | 128.0.0.0–191.255.255.255 | 2 + 14 bits | 16,384 | 16 bits | 65,536 |
| C | 192.0.0.0–223.255.255.255 | 3 + 21 bits | 2,097,152 | 8 bits | 256 |

Even though a class-A address has an 8-bit network part, one of the bits is always 0. Therefore there are only 7 variable bits in the network part, which is why there are only 128 class-A networks, not 256 as you might first expect from an 8-bit network part. Similarly, class-B and class-C addresses have 2 and 3 bits respectively taken up with identifying the class type.

Table 4.1 shows there are only a few class-A networks, but each one can have a huge number of machines on it. At the other end of the scale, there are lots of class-C networks, but relatively few machines on each.

A single IP address can identify an IP address range or network, because the class is uniquely determined by that address, which in turn determines the address range. For example, 192.0.2.29 is a class-C address, so it’s a range of 256 addresses:

192.0.2.0–192.0.2.255

(By convention, the lowest address in the range is used as the network address – 192.0.2.0 in this example.) Now it becomes easy to specify network addresses to be used in the routing decision code described above, e.g.

```
if (dest is part of class-C network 192.0.2.0)
    send the packet to dest directly on interface-1,
    using ARP if necessary
...
else if (dest is part of class-C network 192.168.168.0)
...
```

In practice the number of hosts per network is less than shown in the table because certain addresses are reserved. For example, in the class-C range, addresses 192.0.2.0 and 192.0.2.255 are reserved for use as broadcast addresses (see Module 4.10) so there are only (256 − 2) = 254 IP addresses available for use as real host addresses.

The classes reflect a view of the world-wide IP network as lots of individual networks (each a class A, B or C) owned by different organizations and connected in this way. This system worked well in the early days of the Internet, when it was used by a relatively small number of research and academic institutions. However, as the Internet expanded, the coarse division into huge, medium, and small networks proved too inflexible, and a new mechanism was introduced to give more flexibility, as described in the next module.

## 4.3 From address classes to netmasks

Two problems arose from the coarse division of networks into huge, medium, and small classes:

- 1. an organization with a large number of machines might need to divide its internal network into smaller sub-networks, for several reasons:
  - a single Ethernet segment could not accommodate hundreds of thousands of machines
  - the organization might be spread over several cities or countries
  - certain departments might need special security

The organization will use internal routers of its own to sub-divide its network. How can these sub-networks be specified in routing tables? The addresses class mechanism is of no help here. The organization has been allocated, for example, a single class-B range, so all the internal IP addresses are part of a single range. They really need to sub-divide a single class-B range

- 2. as the Internet has expanded, there is great demand for IP addresses and there aren't enough class A, B and Cs to go around. We'd like to be able to allocate chunks of addresses that closely match an organization's needs, e.g. “a sixteenth of a class B,” or “two class cs,” or whatever.

The first problem (which reared its head) was solved by introducing the concept of sub-netting. You divide up your single, large network into sub-nets. You specify each sub-net using a sub-net mask in combination with an IP address. For example, if your main company network is 10.0.0.0 (class A, giving a range of 10.0.0.0–10.255.255.255), you might sub-divide it as follows:

|  | Network address | Sub-net mask | Resulting address range |
| :-- | :-- | :-- | :-- |
| P | 10.1.1.0 | 255.255.255.0 | 10.1.1.0–10.1.1.255 |
| Q | 10.1.2.0 | 255.255.255.0 | 10.1.2.0–10.1.2.255 |
| R | 10.201.0.0 | 255.255.0.0 | 10.201.0.0–10.201.255.255 |
| S | 10.202.77.0 | 255.255.255.0 | 10.202.77.0–10.202.77.255 |
| T | 10.202.0.0 | 255.255.0.0 | 10.202.0.0–10.202.255.255 |

This gives the network layout shown in Figure 4.3. (The area shown in gray consists of all the 10.x.x.x IP addresses that are not included in any of the specific sub-nets. As we'll see in Modules 6.8–6.12, when you sub-net your network you will often end up with sections of the total range – like the gray area in Figure 4.3 – which you don't use and which don't contain any machines.)

The second problem – how to divide a “class-full” range into smaller pieces – is much more recent, but the technical solution is the same. Instead of using just the IP address when routing (by deriving the network identifier from the address using the address class), routing is done using the IP address and netmask. Therefore, instead of a fixed division of the Internet into class A, B and C networks (huge, medium, small), we can divide the address space into chunks of whatever size is appropriate. For example, you can allocate a sixteenth of a class B to an organization that is large but doesn’t need the 65,536 IP addresses that a full class B offers. This is called Classless Inter-Domain Routing (CIDR). It’s almost universal now – it’s used on the Internet backbone, and on all Windows and Linux systems. The old class-based system continues only in some historical protocols and throughout this book we deal exclusively with CIDR.

![](img/a2132b646d336d5f9a21102d6320e537_120_0.png)

**Figure 4.3 Network layout**

Conveniently (and it’s not a coincidence – this compatibility was designed into the system) you can exactly duplicate the old class A, B, C behavior by considering each class as specifying a default netmask:

| Class | Default netmask |
| :--- | :---: |
| A | 255.0.0.0 |
| B | 255.255.0.0 |
| C | 255.255.255.0 |

In many contexts both Windows-NT and Linux will assume these default netmasks when you enter an address and don’t specify an explicit netmask. Just think of classes as a convenient notation and nothing more.

## 4.4 How netmasks specify ranges of IP addresses

A netmask combined with an IP address specifies a range of IP addresses of a particular size, by selectively extracting the bits of the IP address corresponding to the network part of the address.

A “mask” exposes the interesting parts of something, while covering up the parts you’re not interested in. For example, a semiconductor mask hides parts of a silicon wafer that are not to be exposed to light; when you are decorating, masking tape hides woodwork you want to protect, leaving exposed the pieces you want to paint; the Lone Ranger’s mask hides most of his face leaving only his eyes visible.

A netmask is a type of mask. In fact it’s a bit mask where the 1-bits in the mask indicate the pieces we are interested in, and the 0-bits are the pieces we ignore. (Bit masking is very common in programming. See Web Appendix 2.) The 1-bits in the netmask indicate the part of the IP address that makes up the network part, and the 0-bits indicate the host part. (Or, the netmask hides the host part of an IP address, leaving only the network part of the address visible.) This lets you specify a range of addresses, as follows:

> > given an IP address and a particular netmask, calculate the network part. All the IP addresses that have the same network part (calculated with that netmask) form a set or range of addresses.

Now let’s look at some examples to explain how you use netmasks in practice. Up to now we’ve used only two netmasks, 255.255.255.0 and 255.255.0.0, which are in fact the default netmasks for class C and class B addresses, so we’ll start with those.

### 1. Using mask 255.255.255.0

![](img/a2132b646d336d5f9a21102d6320e537_121_0.png)

The zero byte hides the uninteresting parts, and the three 255 bytes expose the parts we want (because a byte containing 255 has all eight bits set to 1, and none set to 0). In effect, the mask 255.255.255.0 means “ignore the last byte of the IP address; the network part consists of the first three bytes only”. For example:

```
address = 212.140.133.181
netmask = 255.255.255.0
```

gives us a network part of 212.140.133.0 (we just fill in zeros in the parts that we masked off). The range consists of all the IP addresses that have this network part, i.e. all the IP
