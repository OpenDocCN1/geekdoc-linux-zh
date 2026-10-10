Enable IPv6 configuration for this interface: Check here if you are connected to an IPv6 network. (Most networks are still IPV4.)

+   5. On the same window, you must choose whether to get your IP addresses from another computer at boot time or enter the addresses yourself:

Automatically obtain IP address settings with: Select this check box if you have a DHCP or BOOTP server on the network from which you can obtain your computer's IP address, netmask, and gateway. DHCP is the most common way to connect to your ISP. You should consider setting up your own DHCP server if you have more than just a few computers on your LAN. (See Chapter 23 for how to set up a DHCP server.) You can, optionally, set your own host name, which can be just a name (such as *jukebox*) or a fully qualified domain name (such as *jukebox.linuxtoys.net*.)

Statically set IP addresses: If there is no DHCP, or other boot server, on your LAN, you can add necessary IP address information statically by selecting this option and adding the following information:

Address: Type the IP address of this computer into the Address box. This number must be unique on your network. For your private LAN, you can use private IP addresses (see the section, “Understanding IP Addresses” later in this chapter).

Subnet Mask: Enter the netmask to indicate what part of the IP address represents the network. (Netmask is described later in this chapter.)

Default Gateway Address: If a computer or router connected to your LAN is providing routing functions to the Internet or other network, type the IP address of the computer into this box. (Chapter 16 describes how to use NAT or IP masquerading and use Fedora or RHEL as a router.)

Set MTU to: The maximum transfer unit (MTU) sets the number of 8-bit bytes that are available to the Internet Protocol in a link-layer frame. Click the check box and enter a number to change from the default 1500 MTU used by default for Ethernet interfaces in Linux. Lower rates can result in fewer packets being dropped on unreliable networks (some gamers like to lower the rate slightly, so fewer small actions are dropped). Higher rates can improve performance of large data transfers on reliable networks. In most cases, you don't need to modify this.

+   6. Click OK in the Ethernet Device window to save the configuration and close the window.

+   7. Click File → Save to save the information you entered.

+   8. Click Activate in the Network Configuration window to start your connection to the LAN.

# ## Identifying other computers (hosts and DNS)

Each time you use a name to identify a computer, as when browsing the Web or using an e-mail address, the computer name must be translated into an IP address. To resolve names to IP addresses, Fedora and RHEL go through a search order (based on the contents of three files