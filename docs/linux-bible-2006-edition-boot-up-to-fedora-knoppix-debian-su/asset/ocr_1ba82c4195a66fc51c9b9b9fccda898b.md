# Chapter 5 ♦ Getting on the Internet 183

name (such as jukebox) or a fully qualified domain name (such as jukebox.linuxtoys.net).

+   **Statically set IP addresses**—If there is no DHCP or other boot server on your LAN, add necessary IP address information statically by selecting this option and following these steps:

+   **a.** Type the IP address of the computer into the Address box. This number must be unique on your network. For your private LAN, you can use private IP addresses.

+   **b.** Enter the netmask (described later in this chapter) in the Subnet Mask box. The netmask indicates the part of the IP address that represents the network.

+   **c.** Type the IP address of the computer into the Default Gateway Address box if it provides routing functions to the Internet or other network. (Chapter 18 describes how to use NAT or IP Masquerading and how to use Linux as a router.)

+   6. Click OK in the Ethernet Device window to save the configuration and close the window.

+   7. Click File+S to save the information entered.

+   8. Click Activate in the Network Configuration window to start your connection to the LAN.

# Identifying Other Computers (Hosts and DNS)

Each time you need to identify a computer, such as when browsing the Web or using an e-mail address, the computer name must be translated into an IP address. To resolve names to IP addresses, Linux goes through a search order (usually based on the contents of files in `/etc/resolve.conf`, `nsswitch.conf`, and `host.conf`). By default, checks host names (which end up in the `/etc/hosts` file), hosts available via NIS, and host names available via DNS.

Again, for RHEL and Fedora systems, you can use the Network Configuration window to add:

+   **Host names**—You might need to identify hosts on your LAN that are not configured on a DNS server.

+   **DNS search path**—By adding domain names to a search path (such as `linuxtoys.net`), you can browse to a site by its host name (such as `jukebox`), and have Linux search the domains you added to the search path to find the host you are looking for (such as `jukebox.linuxtoys.net`).

+   **DNS name servers**—A DNS server can resolve addresses for the domains it serves and contact other DNS servers to get addresses for all other domains.