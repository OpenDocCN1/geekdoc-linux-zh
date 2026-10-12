onfiguring IP addresses for a handful of servers is a fairly simple task. However, manually configuring IP addresses for an entire department, building, or enterprise of heterogeneous systems can be daunting.

The DHCP (Dynamic Host Configuration Protocol) client and server can assist with these tasks. The client machine is configured to obtain its IP address from the network. When the DHCP client software is started, it broadcasts a request onto the network for an IP address. If all goes well, a DHCP server on the network will respond, issuing an address and other necessary information to complete the client’s network configuration.

Such dynamic addressing is also useful for configuring mobile or temporary machines. Folks who travel from office to office can plug their machines into the local network and obtain an appropriate address for their location.

This module will cover the process of configuring a DHCP server and client. At the end of the module, we’ll step through a complete sample configuration.

# 20.1 **Discovering BOOTP**  
**and the Roots of DHCP**

Once upon a time, when hard disks were expensive, it was fashionable to create diskless machines that would mount their file system across the network from a server that is usually shared. While having diskless stations provided some—mostly financial—advantages, they also presented their own challenges. One of the chicken-and-egg sort of problems with this scheme was how to get enough networking set up to mount remote file systems before you can consult the configuration files that contain your IP address, and so on. One piece of the puzzle was addressed with the Bootstrap Protocol (BOOTP). Each Ethernet network interface

# **Ask the Expert**

**Q: How well will DHCP work with non-Linux systems?**

**A:** DHCP is a standard; thus, any operating system that can communicate with other DHCP servers and clients can work with the Linux DHCP tools. One common solution that includes using the Linux DHCP server component is in office environments where there are a large number of Windows-based clients. The Windows systems can be configured to use DHCP and contact the Linux server to get their IP address. This reduces the need for yet another Windows server and the associated licensing costs surrounding it.