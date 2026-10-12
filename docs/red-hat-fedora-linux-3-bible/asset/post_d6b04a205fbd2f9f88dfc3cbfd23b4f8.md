
The best place to add `iwconfig` options permanently in Fedora is the configuration file for your wireless interface in the `/etc/sysconfig/network-scripts` directory.

Options to `iwconfig` are added to the wireless interface file (such as `ifcfg-eth0` or `ifcfg-eth1`) using the `IWCONFIG` parameter. For example, to add an encryption-key value of 1234-1234-12 for your wireless LAN card, you could add the following line to your wireless-interface file:

```
IWCONFIG="key 1234-1234-12"
```

# Understanding Internet Protocol Addresses

Whether you are using a wired or a wireless network, each computer you communicate with (including yours) must have a unique address on the network. In TCP/IP, each computer must be assigned an Internet Protocol (IP) address. This section gives you some background in IP addresses.

There are two basic ways to assign a host name and IP address to a network interface in Linux:

- **Static addresses** — With static IP addresses, each computer has an IP address that doesn’t change each time the computer reboots or restarts its network interface. This IP address can be entered manually, since it’s not assigned on the fly. You can do this at Fedora installation time, or later using the Network Configuration window.
- **Dynamic addresses** — With dynamic addresses, a client computer gets its IP address assigned from a server on the network when the client boots. The most popular protocol for providing dynamic addresses is called Dynamic Host Configuration Protocol (DHCP). With this method, a client computer may not have the same IP address each time it boots.

| Option | Description |
| :--- | :--- |
| `retry number` | For cards that support MAC retransmissions, you can use this option to determine how many retries are made before the transmission fails. The value can be a number (indicating number of seconds allocated for retries), or a number followed by an m (for milliseconds) or u (for microseconds). Instead of a number, you can set a number of retries using the limit parameter. For example: `retry limit 100` indicates that the transmission can retry up to 100 times. |
| `sens number` | Sets the lowest possible sensitivity threshold for which the wireless interface will try to receive a packet. Raising this level can help block out interference from other wireless LANs that might weakly encroach on your transmission area. |

**TIP:** If you expect to add and remove computers regularly from your LAN or if you have a limited number of IP addresses, you should use DHCP to assign IP addresses. Chapter 23 describes how to set up a DHCP server.

An IP address is a four-part number, with each part represented by a number from 0 to 255 (256 numbers total). Part of that IP address represents the network the computer exists on, while the remainder identifies the specific host on that network. Here’s an example of an IP address:

```
192.168.35.121
```

Originally, IP addresses were grouped together and assigned to an organization that needed IP addresses, based on IP address classes. These days, a more efficient method, referred to as Classless Inter-Domain Routing (CIDR), is used to improve routing and waste fewer IP addresses. These two IP address methods are described in the following sections.

# IP address classes

Unfortunately, it’s not so easy to understand which part of an IP address represents the network and which represents the host without explaining how IP addresses are structured. IP addresses are assigned in the following manner. A network administrator is given a pool of addresses. The administrator can then assign specific host addresses within that pool as new computers are added to the organization’s local network. There were originally three basic classes of IP addresses, each representing a different size network.

- **Class A** — Each Class A address has a number between 0 and 127 as its first part. Host numbers within a Class A network are represented by any combination of numbers in the next three parts. A Class A network therefore contains millions of host numbers (approximately 256 × 256 × 256, with a few special numbers being invalid). A valid Class A network number is:
  - 24
- **Class B** — A Class B IP address has a number between 128 and 191 in its first part. With a Class B network, however, the second part also represents the network. This enables a Class B network to have more than 64,000 host addresses (256 × 256). A valid Class B network number is:
  - 135.84
- **Class C** — A Class C IP address begins with a number between 192 and 223 in its first part. With a Class C network, the first three parts of an IP address represent the network, while only the last part represents a specific host. Thus, each Class C network can have 254 numbers (the numbers 0 and 255 can’t be assigned to hosts). Here is an example of a Class C network number:
  - 194.122.56

To tell your computer which part of a network address is the network and which is the host, you must enter a number that masks the network number. That number is referred to as the *netmask*.

# Understanding netmasks

Suppose you are assigned the Class B address 135.84, but you are only given the pool of numbers available to the address 135.84.118. How do you tell your network that every address beginning with 135.84.118 represents a host on your network, but that other addresses beginning with 135.84 should be routed to another network? You can do this with a netmask.

The netmask essentially identifies the network number for a network. When you assign the IP address that is associated with your computer’s interface to the LAN (eth0), you are asked for a netmask. By default, your computer fills in a number that masks the part of your IP address that represents the class of your network. For example, the default netmasks for Class A, B, and C networks are the following:

- Class A netmask: 255.0.0.0
- Class B netmask: 255.255.0.0
- Class C netmask: 255.255.255.0

Now, if your network was assigned the network number 135.84.118, to tell your computer that 135.84.118 is the network number and not 135.84 (as it normally would be for a Class B address), add a netmask of 255.255.255.0. So you could use host numbers from 1 to 254 (which would go into the fourth part of the number).

To further confuse the issue, you could mask only one or more bits that are part of the IP address. Instead of using the number 255, you could use any other numbers between 0 and 255, including 128, 192, 224, 240, 248, 252, and 254, to mask only part of the numbers in that part of the address.

> NOTE: The reason that only the numbers just mentioned are valid netmasks is that each part is represented by eight binary numbers, but all 1's that are included must be to the left. So 240 would be allowed (11110000) but 242 would not (11110010). This limitation is what lead to the creation of CIDR (see the next section).

# Classless Inter-Domain Routing

The class method of allocating IP addresses had several major drawbacks. First, few organizations fell neatly into one class or another. For most organizations, a Class C address (up to 256 IP addresses) was too small, and a Class B address (up to 65,534 IP addresses) was too big. The result was a lot of wasted numbers in a world where IP addresses were running short. Second, IP classes resulted in too many routing table entries. As a result, routers were becoming overloaded with information.

The Classless Inter-Domain Routing (CIDR) addressing scheme set out to deal with these problems. The scheme is similar to IP address classes, but offers much more flexibility in assigning how much of the 32-bit IP address is the network identifier. Instead of the first 8, 16, or 32 bits identifying the network, 13 to 27 bits could identify the network. As a result, groups of assigned IP addresses could contain from 32 to about 524,000 host addresses.

To indicate the network identifier, a CIDR IP address is followed by a slash (/) and then a number from 13 to 27. A smaller number indicates a network containing more hosts. Here’s an example of an IP address that uses the CIDR notation:

```
128.8.27.18/16
```

In this example, the first 16 bits (128.8) represent the network number, and the remainder (27.18) represents the specific host number. This network number can contain up to 65,536 hosts (the same as a class B address). The following list shows how many hosts can be represented in networks using different numbers to identify the network:

1. /13 524,288 hosts
2. /14 262,144 hosts
3. /15 131,072 hosts
4. /16 65,536 hosts
5. /17 32,768 hosts
6. /18 16,384 hosts
7. /19 8,192 hosts
8. /20 4,096 hosts
9. /21 2,048 hosts
10. /22 1,024 hosts
11. /23 512 hosts
12. /24 256 hosts
13. /25 128 hosts
14. /26 64 hosts
15. /27 32 hosts

The CIDR addressing scheme also helps reduce the routing overload problem by having a single, high-level route represent many lower-level routes. For example, an Internet Service Provider could be assigned a single /13 IP network and assign the 500,000-plus addresses to its customers. Routers outside the ISP would only need to know how to reach the ISP for those half-million addresses. The ISP would then be responsible for maintaining routing information for all of the host routes with that network address.

# Getting IP addresses

So, what is the impact of assigning IP addresses for the computers on your LAN? How you choose which IP addresses to use depends on your situation. If you are part of a large organization, you should get addresses from your network administrator. Even if you don’t connect to other LANs in your organization at the moment, having unique addresses can make it easier to connect to them in the future.
