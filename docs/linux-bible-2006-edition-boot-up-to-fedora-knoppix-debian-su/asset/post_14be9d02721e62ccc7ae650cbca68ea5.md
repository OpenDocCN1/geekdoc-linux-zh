
# Chapter 5 ♦ Getting on the Internet 179

![](img/a2d958d7eab32ca5b89b2b8af808aa70_210_0.png)

**Figure 5-4:** Add servers to a DMZ where they can be more publicly accessible than your desktop systems.

Chapters 24 through 27 explain how to configure different server types, Chapter 18 describes how to set up Linux as a router/firewall. Chapter 18 includes how to configure features such as IP Masking, NAT, and packet forwarding.

## Connecting Other Equipment

I've focused on basic Ethernet and dial-up modems for configuring network connections, Linux supports many other types of network equipment as well as different protocols for communicating over that equipment. Here are a few examples:

- **ISDN**—Integrated Services Digital Network (ISDN) lines were the preferred method of high-speed data lines to small businesses in the United States before DSL became widespread. It is still quite popular in Europe. ISDN forLINUX drivers and tools are available in many Linux systems for connecting to ISDN networks.

- **Token ring**—Although rarely used, token ring network cards are supported. Support for token ring network cards is included in most Linux systems, token rings are rarely used. They were once popular at locations that had IBM systems.

- **PLIP**—It's possible to connect two computers from their parallel ports so that they can communicate using TCP/IP protocols. Parallel Line Internet Protocol (PLIP) requires only a special cable; most Linux systems have built-in software that allows you to log in, transfer files, and perform other activities over that connection.

If your system has Linux source code installed, you can read about supported hardware in the documentation that comes with that source code. On Red Hat and some other Linux systems, the location of kernel documentation for various networking hardware is `/usr/src/linux*/Documentation/networking.

## Using Ethernet Connections to the Internet

- Check whether you have an Ethernet card on your computer (most recent computers have one). If so, connect your Ethernet card to the equipment that gets you the Internet (cable modem, DSL, router/bridge, or network hub/switch). If not, you can purchase an Ethernet card at any retailer that sells computer hardware.
- Ensure that appropriate drivers are available for the card and bring up the interface (typically, the first wired Ethernet card is assigned to the eth0 interface). Simply starting the computer causes the card to be detected and the appropriate driver loaded.
- Get an IP address using DHCP if there is a DHCP server available through the interface. Most ISPs and businesses expect you to connect to their networks using DHCP, so they will provide a DHCP server where you connect your computer to the network.

As long as your desktop system is connected to a network that has a DHCP server to give it an IP address, you can be up and browsing the Web in time.

If you find that the automatic method (DHCP) of connecting to your network doesn’t work, it gets a bit trickier to connect to the Internet. Different Linux distributions offer different tools for manually configuring your Internet connection. The following sections describe a few graphical tools and some command-line and configuration-approaches to configuring wired and wireless network connections.

## Configuring Ethernet During Installation

Many Linux installs ask you if you want to configure your network connection for your Ethernet cards. This is typically for your Ethernet cards and for dial-up modems or other networking equipment. Information you’ll need for (IP address, gateway, DNS server, and so on) is explained in Chapter 7.

When you boot Linux, you can check whether you have access to the Internet by opening a Web browser (such as Mozilla Firefox or Konqueror) and typing in a Web address. If the Web site doesn’t appear in your browser, you’ll need to do some troubleshooting. The “Understanding your Internet Connection” section later in this chapter provides information on how to track down problems with your Internet connection.

## Configuring Ethernet from the Desktop

Most Linux distributions offer graphical tools for configuring network interfaces. These tools step you through the information you need to enter, and then start up the network interface (if you choose) to begin browsing the Web.

Here is a list of tools for configuring network interfaces in a few Linux distributions. Some of these are graphical tools, and some are menu-based:

- **Red Hat Ethernet/Fedora Linux** — The Network Configuration window lets you configure network connection using Ethernet, ISDN, modem, Token Ring, Wireless, and xDSL hardware. The Network Configuration window shows the red hat by selecting System Settings or by picking **system-config** and entering the root password when prompted. (On Red Hat systems, the command is `redhat-config-network`.)

- **SUSE Linux** — The YaST Control Center with SUSE contains features for configuring your network. From the SUSE menu on the panel, select System, then choose Network Devices. The YaST Control Center lets you configure a DSL, ISDN, Modem, or Network Card interface to the network. Select Network Card to configure your wired Ethernet to the Internet.

- **Gentoo Linux** — From a shell (as root user), type **netsetup eth0** to start the menu-driven interface to configure the network connection from your first Ethernet card (eth0). The tool lets you have try to start using DHCP or static address information that you provide.

- **KNOPPIX** — Select the penguin icon in the Knoppix desktop, choose Networking/Internet from the menu. Select the Network card menu entry to configure your network card. Or select from several other network types (ADSL, GPRS, ISDN, Modem).

## Using Network GUI

An example of a graphical tool for configuring your interface is the Network Configuration GUI that comes with Fedora and Red Hat. If you did not configure your LAN connection during installation of Fedora or RHEL, you can do so at any time using the Network Configuration window.

> A computer can have more than one IP address because it has multiple network interfaces. Each network interface must have an IP address to connect to a network. So if you have two Ethernet cards (eth0 and eth1), each needs its own IP address. Also, the address 127.0.0.1 represents the local host.

Here's how to define the IP address for your Ethernet interface in Fedora or RHEL:

1. From the red menu, choose Desktop ⇄ System Settings ⇄ Network or, as root user from a Terminal window, type system-config-network. (If prompted, type the password.) The Network Configuration window appears.
2. Click the Devices tab. A listing of your network interfaces appears.
3. Double-click the eth0 interface (representing your first Ethernet card). A pop-up titled Ethernet Device appears (see Figure 5-5), enabling you to configure your eth0 interface.

4. Activate device when computer starts — Check here to have it start at boot time.
- Allow all users to enable and disable the device — Check to let non-root users enable and disable the network interface.
- Enable IPv6 configuration for this interface — Check here if you are connected to an IPv6 network. (Most networks are still IPv4).

5. You might also choose whether to get your IP addresses from another computer at boot time or enter the addresses yourself:

- Automatically obtain IP address settings—Select this box if you have a DHCP or BOOTP server on the network from which you can obtain your computer's IP address, mask, and gateway. DHCP is recommended if you have more than a couple of computers on your LAN. Optionally, you can set your own host name, which can be just a
