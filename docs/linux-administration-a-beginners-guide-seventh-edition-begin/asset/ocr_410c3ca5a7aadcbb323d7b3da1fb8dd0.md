CHAPTER 12 Network Configuration 351

# How Linux Chooses an IP Address

Now that Linux has two interfaces (192.168.1.15 and 192.168.2.1) in addition to the loop-back interface (127.0.0.1), we can observe Linux will choose a source IP address with which to communicate.

When an application starts, it has the option to bind to an IP address. If the application does not explicitly do so, Linux will automatically choose the IP address on behalf of the application connection-by-connection. When Linux is making the decision, it examines a connection's destination IP address, makes a routing decision based on the route table, and then selects the IP address corresponding to the interface from which the connection will leave. For example, if an application on host A makes a connection to 192.168.1.100, Linux will find that the packet goes out of the eth0 interface, and the source IP for the connection will be 192.168.1.15.

Let us assume that the application chooses to bind to an IP address. If the application is bound to 192.168.2.1, Linux will use that as the source IP address, regardless of which interface the connection will leave. For example, if the application is bound to 192.168.2.1 and a connection is made to 192.168.1.100, the connection leaves out of eth1 (192.168.1.15) with the source IP address of 192.168.2.1. It is now the responsibility of the remote host (192.168.1.100) to know how to send a packet back to 192.168.2.1 (Presumably, the default route for 192.168.1.100 will know how to deal with that).

For hosts that have aliased addresses, a interface may have many IP addresses. For example, we can assign eth0 to 192.168.1.16, eth1 to 192.168.1.17, and eth0:2 to 192.168.1.18. In this case, if the connection leaves the eth0 interface and the application did not bind to a specific interface, Linux will always choose the nonaliased IP address—that is, 192.168.1.15 for eth0. If the application chooses to bind to an IP address—say, 192.168.1.17—Linux will use that IP as the source IP, regardless of whether the connection leaves from eth0 or eth1.

# Hostname Configuration

A system's hostname is the friendly name by which other systems or applications can address the system on a network. Configuring the hostname for a system is therefore an important network configuration task. You would have been prompted to create or choose a hostname for your system during the OS installation. If you didn't specify a hostname during the installation, it is possible that a hostname was automatically assigned to your system.

You should take time to pick and assign hostnames to your servers that best describe their function or role. You should also pick names that can easily scale as your collection of servers grows. Examples of good (or simply playful) and descriptive hostnames are webserver01.example.org, dbserver9.example.com, logger-datacenterB, jupiter.example.org, saturn.example.org, pluto, sergent.example.com, hr-example.com, major.example.org, and so on.