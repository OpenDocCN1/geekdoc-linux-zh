# CHAPTER 34

# Dynamic Host
Configuration Protocol
(DHCP)

D HCP, which stands for *Dynamic Host Configuration Protocol*, is a network protocol that allows a client to obtain its IP address, name server information, gateway server information, and several other network-configuration options from a server that is running a DHCP server.

This chapter will show you how to configure a DHCP client on your FreeBSD system (so that it can obtain an IP address from a DHCP server). It will also show you how to configure a DHCP server.

# How DHCP Works

A detailed discussion of how DHCP works is beyond the scope of this book, but here is a basic rundown of what happens.

In FreeBSD, a client program called `dhclient` allows FreeBSD to act as a DHCP client. When a system configured to use DHCP boots and `dhclient` starts, it will send out broadcast requests on port 68. These requests are sent in UDP format.

If there is a DHCP server on the network, it will be listening to port 68 for these requests. When it receives a request for configuration information, it will check its database for a free IP address that can be assigned to the client. It will then send back all the configuration information that the client requests on port 67, once again using UDP. The IP address that is assigned to the client will be removed from the pool of available addresses so that it is not assigned to another client that requests DHCP configuration information.

# IN THIS CHAPTER

+   * How DHCP Works
+   * Advantages of DHCP over Static IP Addresses
+   * Kernel Configuration for DHCP
+   * Enabling DHCP
+   * The `dhclient` Program
+   * DHCP Server Daemon
+   * Configuring the `dhcpd` Configuration File