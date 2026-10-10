You can get a good overview of the differences between IPv4 and IPv6 policies regard-ing IP address assignments, and the registration process of obtaining IP addresses, by browsing to http://www.arin.net/registry/index.html. Read the Linux IPv6 HOWTO by browsing to http://tldp.org/HOWTO/Linux+IPv6-HOWTO/.

Fedora supports the use of IPv6 and includes a number of networking tools conform-ing to IPv6 addressing. You can configure support for IPv6 by using settings and options in the file named network under the /etc/sysconfig/ directory, along with making changes to related network configuration files, such as /etc/hosts. Many IPv6-based tools, such as ipcalc6, ping6, and traceroute6, are available for Fedora. See various files under the /usr/share/doc/initscripts directory for more informa-tion specific to setting up IPv6 addressing with Linux and Fedora.

Migration to IPv6 is slow in coming, however, because the majority of computer operat-ing systems, software, hardware, firmware, and users are still in the IPv4 mindset. Supporting IPv6 will require rewrites to many networking utilities, portions of operating systems currently in use, and firmware in routing and firewall hardware.

# Dynamic Host Configuration Protocol

As its name implies, Dynamic Host Configuration Protocol (DHCP) configures hosts for connection to your network. DHCP allows a network administrator to configure all TCP/IP parameters for each host as he connects to the network after activation of a NIC. These parameters include automatically assigning an IP address to a NIC, setting name server entries in /etc/resolv.conf, and configuring default routing and gateway informa-tion for a host. This section first describes how to use DHCP to obtain IP address assign-ment for your NIC, and then how to quickly set up and start a DHCP server using Fedora.

> NOTE
> You can learn more about DHCP by reading RFC 2131, “Dynamic Host Configuration Protocol.” Browse to http://www.ietf.org/rfc/rfc2131.txt.

# How DHCP Works

DHCP provides persistent storage of network parameters by holding identifying informa-tion for each network client that might connect to the network. The three most common pairs of identifying information are the following:

+   > - **Network subnet/host address**—Used by hosts to connect to the network at will
+   - **Subnet/hostname**—Enables the specified host to connect to the subnet
+   - **Subnet/hardname address**—Enables a specific client to connect to the network after getting the hostname from DHCP