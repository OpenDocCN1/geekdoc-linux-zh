> **CROSS-REFERENCE:** Chapter 23 describes the NIS client and server software.

# Dynamic Host Configuration Protocol server

Instead of going to each computer on your local network and adding all the TCP/IP information they need in order to work (IP address, netmasks, gateways, and so on), you can configure Red Hat Linux as a Dynamic Host Configuration Protocol (DHCP) server to distribute that information. The client computer simply identifies the IP address of the DHCP server so that when the client starts up its network connection, the DHCP server automatically assigns its network address.

By default, DHCP is turned off. To turn it on, type `chkconfig dhcpd on`. Besides starting the service, you must also configure the `/etc/dhcpd.conf` file.

> **CROSS-REFERENCE:** Chapter 23 describes how to set up a DHCP server.

# Lightweight Directory Access Protocol server

If your organization uses Lightweight Directory Access Protocol (LDAP) databases of information, running the LDAP server that comes with Red Hat Linux enables you to access those databases. Likewise, the LDAP server lets you use LDAP-enabled applications, such as Netscape Roaming Access and sendmail 8.

By default, the LDAP service is turned off. To turn it on, type `chkconfig ldap on`. In addition to running the start-up script, you must configure files in the `/etc/ldap/` directory.

# Domain Name System server

A Domain Name System (DNS) server is set up to translate host names to IP addresses on a TCP/IP network. Red Hat Linux can be configured as a DNS server using the named daemon.

By default, the DNS server is not configured to start automatically in Red Hat Linux. To start a DNS server, type `chkconfig named on`. In addition to starting the service, you must configure the `/etc/named.conf` file and configure zone files (in the `/var/named` directory).

# Reverse Address Resolution Protocol server

The Reverse Address Resolution Protocol (RARP) daemon responds to requests from RARP clients that must obtain their own IP addresses. Today, RARP is not used very often.

By default, the RARP service is off. To start an RARP server, type `chkconfig rarpd on`. When requests come in for addresses, the `/usr/sbin/rarpd` daemon checks the `/etc/ethers` or NIS+ databases for addresses.