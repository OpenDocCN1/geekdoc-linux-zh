# **Consider Cache**

A caching-only name server holds recent name resolution query results in its memory. If you are only employing client-side DNS, consider configuring your system to be a caching-only server, using software such as `dnsmasq`. By caching name resolutions, resolving speeds can improve significantly.

# **Secondary Server**

If you are managing a DNS server for your company, besides a primary server, consider configuring a secondary server. This name server receives its information from the primary server and can increase name resolution performance by offloading the primary server’s burden.

# # Configuring It Right

Network configuration was covered in Chapter 7. However, there are a few additional special topics that may help you with troubleshooting.

# **Interface Configurations**

Being able to view a NIC’s configuration and status is important in the troubleshooting process. You may need to view its IP address, its MAC address, subnet configuration, error rates, and so on. In addition, understanding configuration items such as whether or not a NIC has a static or DHCP-provided IP address is part of this process.

Be aware that if you use NetworkManager on a system with `firewalld` as its firewall service, when a new network device is added, it will automatically be added to the `firewalld` default zone. If the default zone is set to `public`, the network device will only accept selected incoming network connections. See Chapter 18, “Overseeing Linux Firewalls,” for more details on `firewalld`.

# **Ports and Sockets**

Ports and sockets are important structures in Linux networking. Understanding the difference between the two will help in the troubleshooting process.

A *port* is a number used by protocols, such as TCP and UDP, to identify which service or application is transmitting data. For example, port 22 is a well-known port designated for OpenSSH, and DNS listens on port 53. TCP and UDP packets contain both the packet’s source and destination ports in their headers.

A program connection to a port is a *socket*. A *network socket* is a single endpoint of a network connection’s two endpoints. That single endpoint is on the local system and bound to a particular port. Thus, a network socket uses a combination of an IP address (the local system) and a port number.

# **Localhost vs. a Unix Socket**

The localhost designation and a Unix socket are often used for services, such as SQL. Being able to differentiate between the two is helpful.

Localhost is the hostname for the *local loopback interface*, which was first described in Chapter 7. Localhost uses the IPv4 address of 127.0.0.1 and the IPv6 address of ::1. Basically, it allows programs on the current system to test or implement networking services via TCP without needing to employ external networking structures.