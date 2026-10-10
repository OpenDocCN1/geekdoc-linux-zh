IP addresses dynamically. Thus, if your network has many servers that need static IP addresses, using DHCP may not reduce your administrative effort.

+   - **Multiboot or variable configurations** If many computers on the network multiboot between multiple OSs, or if they're used for testing OS installations, DHCP can be particularly beneficial because DHCP saves effort for each OS or installation, not just each physical computer.

+   - **Transient computers** If your network hosts computers that come and go, such as laptops, using DHCP can greatly simplify your configuration. This is particularly true if the laptops routinely connect to several different networks; if all the networks use DHCP, a single configuration on a laptop can work on all the networks to which it connects.

+   - **User-configured systems** If end users configure their own computers, using DHCP can reduce the chance of a misconfiguration.

+   - **Too many computers** If you have more computers than IP addresses, but if not all computers are in use at all times, DHCP can help you get by. The server can assign an IP address to one computer, and then when it shuts down, the address becomes available for reassignment. To work best in such an environment, you need to set a short lease time (described in the upcoming section, "Setting Global Options").

> **Tip**
> Network Address Translation (NAT), described in Chapter 17, is another technique for stretching a limited supply of IP addresses. NAT enables use of more computers than you have IP addresses even if all the computers are in use at once.

On the whole, DHCP is best used on networks with more than half a dozen or a dozen computers, or when the computers on the network change frequently. It's of least value on very small networks or when most of the computers on the network require static IP addresses.

In a standard configuration, a DHCP server responds to *broadcasts* from clients—packets addressed to all computers on a network. DHCP works in this way because a DHCP client doesn't have an IP address when it first boots, nor does it know the address of a DHCP server. Thus, a broadcast will reach the DHCP server if it's on the local subnet. For this reason, if your network is large enough to include routers between multiple subnets, you'll either need a DHCP server on each subnet or a special router configuration to echo such requests between subnets.

# ## Installing a DHCP Server

The most common DHCP server for FreeBSD is the Internet Software Consortium (ISC) DHCP server. You can install this server from either the packages or the ports system, as described in Chapter 11 (it's called `isc-dhcpd`).