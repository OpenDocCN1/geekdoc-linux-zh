# CHAPTER 12 | Managing Networking

> IMPORTANT
A typical Red Hat Enterprise Linux 8 machine configured to get IPv4 addresses through DHCP is usually also configured with SLAAC to get IPv6 addresses. This can result in SLAAC unexpectedly obtaining IPv6 addresses when an IPv6 router is added to the network.

Some IPv6 deployments combine SLAAC and DHCPv6, using SLAAC to provide only network address information and DHCPv6 to provide other information, such as which DNS servers and search domains to configure.

# HOST NAMES AND IP ADDRESSES

It would be inconvenient if you always had to use IP addresses to contact your servers. Humans generally would prefer to work with names than long and hard-to-remember strings of numbers. And so Linux has a number of mechanisms to map a host name to an IP address, collectively called name resolution.

One way is to set a static entry for each name in the /etc/hosts file on each system. This requires you to manually update each server's copy of the file.

For most hosts, you can look up the address for a host name (or a host name from an address) from a network service called the Domain Name System (DNS). DNS is a distributed network of servers providing mappings of host names to IP addresses. In order for name service to work, a host needs to be pointed at a nameserver. This nameserver does not need to be on the same subnet; it just needs to be reachable by the host. This is typically configured through DHCP or a static setting in a file called /etc/resolv.conf. Later sections of this chapter will discuss how to configure name resolution.