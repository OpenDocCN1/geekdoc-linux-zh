# SETTING UP A SERVER

+   - A new user can set up an Internet connection without dealing with IP addresses, netmasks, DNS addresses, and other technical details. Experienced user can set up a connection more quickly.

+   - DHCP facilitates assignment and management of IP addresses and related network information by centralizing the process on a server. A system administrator can configure new systems, including laptops that connect to the network from different locations, to use DHCP; DHCP assigns IP addresses only when each system connects to the network. The pool of IP addresses is managed as a group on the DHCP server.

+   - DHCP facilitates the use of IP addresses by more than one system, reducing the total number of IP addresses needed. This conservation of addresses is important because the Internet is quickly running out of IPv4 addresses. Although a particular IP address can be used by only one system at a time, many end-user systems require addresses occasionally, when they connect to the Internet. By reusing IP addresses, DHCP has lengthened the life of the IPv4 protocol. DHCP applies to IPv4 only, as IPv6 (page 387) forces systems to configure their IP addresses automatically (called autoconfiguration) when they connect to a network.

DHCP is particularly useful for an administrator who is responsible for maintaining a large number of systems because individuals no longer need to store unique configuration information. With DHCP, the administrator can set up a master system and deploy new systems with a copy of the master's disk. In educational establishments and other open-access facilities, the hard image may be stored on a shared drive, which can work automatically restoring itself to pristine condition at the end of each day.

# MORE INFORMATION

Web www.dhcp.org
DHCP FAQ: www.dhcp-handbook.com/dhcp_faq.html

HOWTO DHCP Mini HowTO

# How DHCP Works

Using DHCP, the client contacts the server daemon, dhcpd, to obtain the IP address, broadcast address, nameserver address, and other networking parameters. In turn, the server provides a lease on an IP to the client. The client can request the specific terms of the lease, including its duration; the server can limit these terms. While connected to the network, a client typically requests extensions of its lease as necessary so its IP address remains the same. This lease may expire when the client is disconnected from the network, with the server giving the client a new IP address when it requests a lease. You can also set up a DHCP server to provide static IP addresses for specific clients (refer to “Static Dynamic IP Addresses” on page 382). DHCP is broadcast based, so both client and server must be on the same subnet (page 385).