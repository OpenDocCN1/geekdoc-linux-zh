# 668 Part IV: Fedora RHEL Network and Server Setup

The best place to add iwconfig options permanently in Fedora or RHEL is the configuration file for your wireless interface in the /etc/sysconfig/network-scripts directory.

Options to iwconfig are added to the wireless interface (such as ifcfg-eth0 or ifcfg-eth1) using the IWCONFIG parameter. For example, to add an encryption-key value of 1234-1234-12 for your wireless LAN card, you can add the following line to your wireless-interface:

```
IWCONFIG="key 1234-1234-12"
```

# Understanding Internet Protocol Addresses

Whether you are using a wired or a wireless network, each computer you communicate (including yours) has a unique address on the network. In TCP/IP, each computer must be assigned an Internet Protocol (IP) address. This section gives you some background in IP addresses.

There are two ways to assign a hostname and IP address to a network interface in Linux:

+   - Static addresses — With static addresses, each computer has an IP address that doesn't change when the computer reboots or restarts its network interface. Its IP address can be entered manually because it's not on-the-fly. You can do this at Fedora or RHEL installation time, or later using the Network Configuration window.

+   - Dynamic addresses — With dynamic addresses, a client computer gets its IP address assigned from a server on the network when the client boots. The most popular protocol is called Dynamic Host Configuration Protocol (DHCP). With this method, a client computer may not have the same IP address each time it boots.

> TIP: If you expect to add and remove computers regularly from your LAN or if you have a limited number of IP addresses, you should use DHCP to assign IP addresses. Chapter 23 describes how to set up a DHCP server.

An IP address is a four-part number, with each part represented by a number from 0 to 255 (256 numbers total). Part of that IP address represents the network the computer exists on, while the remainder identifies the specific host on that network. Here's an example of an IP address:

```
192.168.35.121
```

Originally, IP addresses were grouped together and assigned to an organization that needed IP addresses, based on IP address classes. These days, a more efficient method, referred to as Classless Inter-Domain Routing (CIDR), is used to improve routing and waste fewer IP addresses. These two IP address methods are described in the following sections.