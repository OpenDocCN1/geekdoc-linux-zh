# Chapter 15: Setting Up Network Connections and LANs 647

have Linux the domains you added to the search path to find the host you are looking for (such as jukebox.linutoys.net).

+   DNS servers. A DNS server can resolve addresses for the domains it serves and contact other DNS servers to get addresses for all other DNS domains.

> NOTE: If you are configuring a DNS server, you can use that server to centrally store names and IP addresses for your LAN. This saves you the trouble of updating every computer's /etc/hosts file time you add or change a computer on your LAN. Refer to Chapter 25 to learn how to set up a DNS server.

To add hosts, IP addresses, search paths, and DNS servers, do the following:

+   Start the Network Configuration. As root user from a Terminal window, type system-config-network or from the Desktop menu, click System Settings -> Network. The Network Configuration window appears.

+   Click the Hosts tab. A pop-up window appears you to add the list of IP addresses, hostnames, and aliases appears.

+   Click New. A pop-up window appears you to add the IP address, hostname, and aliases for a host that you can reach on your network. Figure 15-11 shows the Network Configuration window and the pop-up window for adding a host.

![](bbox=[0.282, 0.423, 0.653, 0.718])

Figure 15-11: Add hosts to /etc/hosts using the Network Configuration window.

+   Type in the IP address number, hostname, and optionally, the host alias.

+   Click OK.

+   Repeat this process until you have added every computer on your LAN.

+   Click the DNS tab.