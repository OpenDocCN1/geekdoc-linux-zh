leased; and at the end of the lease, the network client can extend or relinquish the lease. The advantage of DHCP for a company is that the method of assigning IP address is automatic; hence, a duplicate IP address is unlikely to be assigned. In addition, if you have limited IP addresses, DHCP can maximize the use of each of them by allocating addresses, as and when needed. Servers are not usually configured using temporary DHCP leases, as you will always want these to be *static addresses* so that they can be linked with DNS. The DHCP server maintains a list of the leases in a file called *dhcpd.leases*, usually in */var/db*.

When you install Linux as a server, the option to install the DHCP server software will be listed. After installation, the DHCP server can be added easily from a number of Web sites or via the *install software*, which will be present in most distributions. The complexity in setting up of a DHCP server will depend upon your network architecture and the amount you want the DHCP server to do. The following will outline the basics for setting up the server, which will be a good basic introduction into the subject.

# **DHCP Server Configuration**

Before starting to configure the DHCP server, it is very important to understand your network and what parameters you will be configuring. The following are the basic parameters you will need to configure:

+   - Domain name
+   - DNS servers
+   - Lease times
+   - Routing
+   - Static IP addresses
+   - Logging
+   - Primary or secondary DHCP server

If you have a large network with many servers, you may wish to allocate a contiguous subnet for these servers to make the allocation of IP addresses easier. In addition, there will be some users who need a static IP address, perhaps to allow them to have specific access rules in a router or firewall. These should also be grouped together whenever possible to make the configuration tables more readable. The configuration file for DHCP is /etc/dhcpd.conf, and a sample file is included when you install the DHCP server.

Each subnet that you are going to provide DHCP services for must be defined in the file. The main options that can be used are described below.