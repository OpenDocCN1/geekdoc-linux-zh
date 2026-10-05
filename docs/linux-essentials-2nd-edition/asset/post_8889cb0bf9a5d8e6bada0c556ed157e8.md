
## Configuring a Network Connection

Router A router (also known as a gateway) connects two or more networks together. Your desktop or server computer is likely to connect directly to a handful of computers, including a router. The router links to another network, which in turn links to another, and so on. To contact a computer on another network, your computer communicates through the router. Homes and small businesses use some broadband routers to connect to the Internet. Such devices perform routing and have built-in DNS, DHCP, and other useful services.

> Certification Objective
> TCP/IP The Transmission Control Protocol/Internet Protocol (TCP/IP) is a set of standards that underlies most modern network communications in the software-level.

> Wi-Fi This term applies to the common forms of wireless networking, more properly known as IEEE 802.11. Several variants are available that differ in speed. The, "Creating a Wi-Fi Connection," in this chapter, describes Wi-Fi configuration in more detail.

The process of creating a network connection is one of assigning the IP address and associated netmask. Using the IP address, the computer can communicate with other computers on the local network—that is, anything that doesn't require a router as an intermediary. In some cases, you will need to tell the computer about the network's router so that it can communicate with other network segments (often including the entire Internet). Giving your computer the IP address of a DNS server will enable you to specify computer hostnames rather than IP addresses, which is a highly desirable feature. These four features—the IP address, the netmask, the router's IP address, and the DNS server's IP address—constitute the basic network configuration features.

In most cases, DHCP can dish out these features. This can make network configuration fairly automatically, as you'll see in this chapter. If your network doesn't support DHCP, though, you'll need to contact your network's administrator to obtain the critical configuration information. In some cases, you will need still more information. For instance, if you're using Wi-Fi, you'll need to know the Wi-Fi network's name and perhaps its password.

In most cases, your network connection will come up automatically (nearly so). Sometimes, though, you'll have to adjust the configuration manually or simply activate it. If available, automatic configuration is handled via DHCP, so we begin by describing it in more detail.

> Several alternatives to TCP/IP exist, such as AppleTalk, NetBEUI, and IPX/SPX. TCP/IP, however, is the most common network protocol, and the one that underlies the Internet.

We then cover a topic that's applicable to only some systems: configuring Wi-Fi. If you use it, you must configure Wi-Fi before setting other network options. Once Wi-Fi is configured, the rest of the network setup procedure is much like for wired networks. We then provide an example of using GUI tools for network configuration. These tools are easy to use, and they can handle most situations. Finally, we cover text-based configuration tools, which provide a great deal of power that you might need to use in certain settings.

## Deciding Whether to Use DHCP

As noted earlier, a computer requires, at a minimum, two pieces of information to connect to a typical network: an IP address and a netmask. IP addresses for a router and a DNS server are practical on most networks, although in some cases you do without one or both. Some networks require additional configuration details.

Configuring every computer on a large network with all of this information can be time-consuming. Worse, it can lead to problems caused by human errors, such as types in IP addresses. For this reason, most networks provide a DHCP server, which can provide this information to other computers.

Depending on the configuration of the server, DHCP can be used to deliver IP addresses in one of two ways:

- In a fixed way, so that each computer receives the same IP address every time it boots
- Dynamically, so that a single computer might receive different IP addresses on different boots

Which is a policy detail for your network administrator. You needn't need to be concerned with it, except to know that a computer configured with DHCP is not necessarily guaranteed to receive the same IP address on each boot. This fact can have important implications. In instance, it's easily guaranteed and most reliable to configure a server computer if it has a fixed IP address. Thus, as a matter of policy, server computers are often configured without using DHCP—even if workstations on the same network use DHCP. This isn't always the case, though—as already noted, DHCP can deliver a fixed address to some or all computers, so that the DHCP server's administrator can configure a network's servers in this way.

As a practical matter, unless you're configuring your own private network, you should ask your network administrator whether to use DHCP for a new computer. If the answer is no, you should ask for an IP address, the netmask, the router's IP address, and the DNS server's IP.

![](img/77662199428609b7662c8dc9c0e45c10_309_0.png)

## Creating a Wi-Fi Connection

Wi-Fi connections are most often used on laptop and smaller portable computers, since using such devices without a physical network cable is often desirable. Some desktop computers, though, have Wi-Fi capabilities, and you may want to use them.

Before proceeding, be aware that you may have access to a Wi-Fi network. If you're configuring a computer to connect to a broadband router that you've purchased and set up, consult the router's documentation to learn how to locate the router's critical information, such as the service set identifier, or SSID (the Wi-Fi network's name, which may be distinct from the TCP/IP network name), and the password it use. If you're trying to connect to a business network or a public network, consult the network administrator to obtain this information.

Whatever the computer type, the easiest method of configuring your Wi-Fi connection is to use the GUI. Details of how to do this from one distribution to another. As an example, consider the task in Fedora:

1. Open the System Settings by clicking the down-arrow in the upper-right corner of the desktop and selecting the System Settings from the resulting menu (the crossed tools) or by typing gnome-control-center at a shell prompt.
2. Click the Network item in the System Settings Hardware section. The window that appears is shown in Figure 15.1.

> The procedure described here is equivalent to plugging an Ethernet cable into an Ethernet port. This procedure might or not set up TCP/IP options.

![](img/77662199428609b7662c8dc9c0e45c10_310_0.png)

FIGURE 15.1 You can adjust the most common network settings from the Network item in the System Settings menu.

# Chapter 15 · Managing Network Connections

If you don't see a wireless option, you may lack Linux drivers for your Wi-Fi hardware. Consult the sidebar "Obtaining Wi-Fi Drivers" for advice on resolving this problem.

3. Click Wi-Fi in the list on the left side of the Network window.
4. Select your network from the list. If the network requires authentication, a dialog box like the one shown in Figure 15.2 will appear.

![](img/77662199428609b7662c8dc9c0e45c10_311_0.png)

FIGURE 15.2 If your Wi-Fi network requires authentication, you must enter a password before you can begin using it.

5. Type your network's password in the Password field and then click Connect.

The network entry in the Network window (see Figure 15.1) should now show that the workstation is connected to that network. Click the gear icon next to the Wi-Fi network name to see the IP address, the default route, and the DNS server's IP address assigned to your system. The computer is now completely configured for network access—the utility has automatically performed the tasks described in the section "Using a Network Configuration GUI," later in this. If not, though, you may need to perform additional configuration tasks, such as manually setting an IP address. It's also possible that the Wi-Fi connection has failed.

## WI-FI SECURITY

Because Wi-Fi data is carried over radio waves, it's easy for the transmissions to be intercepted. Somebody sitting in a car outside a building can often gain access to a Wi-Fi network, which poses three problems:
