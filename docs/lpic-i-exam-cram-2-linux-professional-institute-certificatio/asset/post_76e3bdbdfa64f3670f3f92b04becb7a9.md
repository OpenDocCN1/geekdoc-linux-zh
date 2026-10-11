
# Basic Networking

**Terms you'll need to understand:**

- ✔ Broadcast address
- ✔ DHCP
- ✔ IP (Internet Protocol)
- ✔ Network address
- ✔ Network interface
- ✔ Network mask
- ✔ PPP
- ✔ Routing table

**Techniques you'll need to master:**

- ✔ Understanding basic networking
- ✔ Identifying hosts on a network
- ✔ Determining addresses
- ✔ Viewing, changing, and verifying interface configurations
- ✔ Configuring IPs manually or statically
- ✔ Configuring gateway addresses
- ✔ Viewing, changing, or correcting routing table entries
- ✔ Troubleshooting network problems
- ✔ Configuring a PPP client
- ✔ Initializing and connecting via a PPP link

## Conceptual Overview of Networking

An Internet Protocol (IP) is a unique address or locator for a host on a network or on the Internet. All machines and internetworking devices that communicate via Transmission Control Protocol/Internet Protocol (TCP/IP) have an IP they are known by and communicated through.

To understand how all this works, think of the Internet, which is a large network made up of many interconnected smaller networks. The smallest building block of a network is the host, or any machine that has an IP and could respond to a ping.

Hosts are considered standalone unless they are connected to a network, and a logical grouping of hosts on a network is usually known as a subnet.

The difference between a subnet and a segment is that a subnet is a logical grouping of hosts, based on their addressing, whereas a segment is usually a physical grouping of hosts that are attached to the same wire, hub, or switch.

When trying to understand the concepts of networks and hosts, think of a network as a street that has houses on it that represent hosts. If you wanted to find a particular house, you could very well go to that street and begin looking up and down it at the house numbers. Figure 17.1 illustrates a network as a street and hosts as houses.

![](img/49f4f38f3aec011238fa50f89e643db3_449_0.png)

**Figure 17.1** Networks and hosts.

Following the analogy of networks being streets and hosts on those networks being houses on the streets, an intersection between two streets would be similar to a router or gateway between networks.

In this day of subnet calculators and IBM's *Linux Watch*, the temptation would be to skip some of this information. None of this is blue-sky knowledge; it's all applicable to the exam and in most cases to real-life work on a daily basis for a network sysadmin.

## Necessary Configuration Information

To participate in more than a single subnet or network, a host needs to have three things:

- **IP**—Assigned either statically or dynamically, the address must be valid to work.
- **Network mask**—Each logical network or subnet has a particular network mask that helps define where one section of addresses ends and another begins. This is also known as the *subnet mask*, particularly in a Microsoft environment.
- **Gateway address**—Like a door leading out of a room, a gateway address is the local IP associated with a network card or interface on a gateway or router device. Hosts configured with this address as the default gateway send traffic to this address when they need to access remote hosts.

## IPs

An IPv4 IP consists of 32 bits grouped in four octets of 8 bits, with each octet separated by a dot. This is also known as a *dotted quad*. A particular IP, such as 192.168.10.100, would be expressed as the bit values shown here:

`11000000.10101000.00001010.01100100`

Bits in an octet have a specific value, and each octet's bits have the values shown in Figure 17.2.

| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|---|---|---|---|---|---|---|---|

**Figure 17.2 Bit values in an octet.**

When a bit in an octet is turned on, that value is added to any other bit values that are turned on to make a decimal number. With the way the bits are arranged, there is only one bit pattern to make any given number.

It might help to visualize these bits as a bank of light switches, each representing a particular value of watts. For example, if you had a bank of light switches with corresponding wattage, you would turn on the switches for **64**, **32**, and **4** to produce **100** watts of light. Figure 17.3 shows how this would look.

![](img/49f4f38f3aec011238fa50f89e643db3_451_0.png)

Typically, you'll be working with IPs that have been assigned by a higher authority—either your IT department or corporate headquarters, or even an Internet service provider (ISP).

## Networks and Hosts

The basic tenet of all networking with IPs is that there will be two portions to any given address that are assigned. Using the previous *streets = networks and houses = hosts* analogy, you could look at a host's address, such as **192.168.1.200**, as being broken up into two parts: the street or network address (**192.168.1**) and the house or host address (**.200**).

Just as houses on the same street use that street as part of their addresses, a host address is treated as belonging to the network address it shares with the other hosts that belong to that network.

## Address Class Ranges

Five address class ranges are defined by a request for comment (RFC 1918). An address class range is defined by the bit pattern of the first two or three bits in the first octet. This is important because the address class determines the number of hosts that are possible by default for each of the resulting networks.

> **NOTE** A request for comment (RFC) documents specifications for Internet standards. As a draft for a particular specification is evaluated, it goes through a process that ends with it becoming an RFC, which is similar to a standard but is often treated as a very firm suggestion.

The five address classes are as follows:

- **A**—From 1 to 126; each of these encompasses 16,777,216 host addresses. There can be 126 Class A networks.
- **B**—From 128 to 191; each of these encompasses 65,536 host addresses. There can be 16,382 Class B networks.
- **C**—From 192 to 223; each of these encompasses 254 host addresses. There can be 2,097,150 Class C networks.
- **D**—From 224 to 239. This range is reserved for such activities as multicast and is not usually available for host addresses.
- **E**—From 240 to 254; this range is reserved for future use.

For those who are asking where the 127 range is, the designers saw fit to leave the entire 127 range for loopback or local host networking only. Yes, that’s 16,777,216 addresses all so someone can ping his local host to see whether IP is working!

![](img/49f4f38f3aec011238fa50f89e643db3_452_0.png)

> Remember that when looking at the massive expanse of IPs available for Class A and Class B address ranges, those are typically broken up into many smaller networks by the use of custom subnet masks, which are covered later in the chapter.

## Using the Bits to Determine Class

If you look at the bit pattern for the first octet of an address that’s a Class A, you’ll see the first bit must always be off because no Class A address is above a 126 in the first octet:

`1 = 01000000`

In a similar fashion, a Class B address cannot have the first bit in the first octet on. All Class B addresses range from 128 and higher:

`128 = 10000000`

By the same token, no Class C address can exist without the first two bits in the first octet set to on. All Class C addresses range from 192 and higher:

`192 = 11000000`

## Network Masks

I’ve long said that one way to understand IPs and their partner network (or subnet) masks is to think of every IP as consisting of two pieces: a network section and a host section. The network mask sets where network bits end and host-assignable bits begin.

For each class, the point at which a network mask stops is where the network portion of an address ends and the host-assignable portion begins. For example, if you take the address 192.168.1.200 and a default subnet mask, the first three octets represent the network and the last octet is where hosts can be assigned.

Address class ranges come with their own built-in default subnet mask; only one can be the default per range:

- **A**—255.0.0.0 or /8 for the number of bits that represent the network mask
- **B**—255.255.0.0 or /16 for the number of bits that represent the network mask
- **C**—255.255.255.0 or /24 for the number of bits that represent the network mask

![](img/49f4f38f3aec011238fa50f89e643db3_453_0.png)

> LPI follows the industry in its use of either fully spelled-out network masks (255.255.255.0) or using abbreviated notation (/24) to represent any network mask assigned to a host or set of hosts. The number 24 relates to the number of bits used for the subnet mask.
>
> Be prepared to solve questions that use either method of expressing the network mask.

## Using Default Network Masks

As previously mentioned, the place where the network portion of an address ends is where the subnet mask bits stop. If you have a network address such as 192.168.10.0 and a default subnet mask of 255.255.255.0 or /24, a single network (192.168.10.0) exists and the remaining 8 bits that are outside the network portion are available for assignment to hosts.

It might help to express the network address and then the network mask as a set of bits, like so:

```text
11000000 . 10101000 . 00001010 . 00000010   (The IP)
11111111 . 11111111 . 11111111 . 00000000   (The Subnet Mask)
```

Because the network mask is a /24, or default Class C network mask, you can easily see where the network begins and ends and what’s usable for host addresses. The boundary in this example is the last dot, leaving 8 bits worth of addresses for this single network assignable to hosts.
