
## Network Configuration

If you did not configure your LAN connection during installation of Linux, you can do so at any time using the Network Configuration window (`neat` command). The IP address and host names can be assigned statically to an Ethernet interface or retrieved dynamically at boot time from a DHCP server.

> **NOTE:** A computer can have more than one IP address because it can have multiple network interfaces. Each network interface must have an IP address (even if the address is assigned temporarily). So, if you have two Ethernet cards (`eth0` and `eth1`), each needs its own IP address. Also, the address `127.0.0.1` represents the local host, so users on the local computer can access services in loopback.

To define your IP address for your Ethernet interface, follow this procedure:

1. Start the *Network Configuration*. From the red hat menu, click **System Settings → Network** or, as root user from a Terminal window, type `neat`. (If prompted, type the root password.) The Network Configuration window appears.
2. Click the **Devices** tab. A listing of your existing network interfaces appears.
3. Double-click the `eth0` interface (representing your first Ethernet card). A pop-up window appears, enabling you to configure your `eth0` interface. Figure 15-6 shows the Network Configuration window and the pop-up Ethernet Device window configuring `eth0`.

![](img/b22364e57409c2481ba806e4e6b9309c_614_0.png)

4. On the Ethernet Device window that appears, you can enter the following information:
   - **Activate device when computer starts:** Check here to have `eth0` start at boot time.
   - **Allow all users to enable and disable the device**: Check to let non-root users enable and disable the network interface.
   - **Enable IPv6 configuration for this interface**: Check here if you are connected to an IPv6 network. (Most networks are still IPv4.)
5. On the same window, you must choose whether to get your IP addresses from another computer at boot time or enter the address yourself:
   - **Automatically obtain IP address settings with**: Select this box if you have a DHCP or BOOTP server on the network from which you can obtain your computer’s IP address, netmask, and gateway. DHCP is recommended if you have more than just a couple of computers on your LAN. (See Chapter 23 for how to set up a DHCP server.)
     - You can, optionally, set your own host name, which can be just a name (such as `jukebox`) or a fully qualified domain name (such as `jukebox.linuxtoys.net`).
   - **Statically set IP addresses**: If there is no DHCP, or other boot server, on your LAN, you can add necessary IP address information statically by selecting this option and adding the following information:
     - **Address**: Type the IP address of this computer into the Address box. This number must be unique on your network. For your private LAN, you can use private IP addresses (see the section, “Understanding IP Addresses” later in this chapter).
     - **Subnet Mask**: Enter the netmask to indicate what part of the IP address represents the network. (Netmask is described later in this chapter.)
     - **Default Gateway Address**: If a computer or router connected to your LAN is providing routing functions to the Internet or other network, type the IP address of the computer into this box. (Chapter 16 describes how to use NAT or IP masquerading and use Fedora as a router.)
6. Click OK in the Ethernet Device window to save the configuration and close the window.
7. Click File → Save to save the information you entered.
8. Click Activate in the Network Configuration window to start your connection to the LAN.

## Identifying other computers (hosts and DNS)

Each time you use a name to identify a computer, as when browsing the Web or using an e-mail address, the computer name must be translated into an IP address. To resolve names to IP addresses, Fedora goes through a search order (based on the contents of three files in `/etc`: `resolv.conf`, `nsswitch.conf`, and `host.conf`). By default, it checks:

- Host names you add yourself (which end up in the `/etc/hosts` file).
- Hosts available via NIS (if an NIS server is configured as described in Chapter 23).
- Host names available via DNS.

You can use the Network Configuration window to add:

- Host names and IP addresses. You might do this to identify hosts on your LAN that are not configured on a DNS server.
- DNS search path. By adding domain names to a search path (such as `linuxtoys.net`), you can browse to a site by its host name (such as `jukebox`), and have Linux search the domains you added to the search path to find the host you are looking for (such as `jukebox.linuxtoys.net`).
- DNS name servers. A DNS server can resolve addresses for the domains it serves and contact other DNS servers to get addresses for all other DNS domains.

> **NOTES:** If you are configuring a DNS server, you can use that server to centrally store names and IP addresses for your LAN. This saves you the trouble of updating every computer's `/etc/hosts` file every time you add or change a computer on your LAN. Refer to Chapter 25 to learn how to set up a DNS server.

To add host names, IP addresses, search paths, and DNS servers, do the following:

1. Start the Network Configuration. As root user from a Terminal window, type `neat` or from the red hat menu, click System Settings → Network. The Network Configuration window appears.
2. Click the **Hosts** tab. A list of IP addresses, host names, and aliases appears.
3. Click **New**. A pop-up window appears asking you to add the IP address, host name, and aliases for a host that you can reach on your network. Figure 15-7 shows the Network Configuration window and the pop-up window for adding a host.

![](img/b22364e57409c2481ba806e4e6b9309c_616_0.png)

4. Type in the IP address number, host name, and, optionally, the host alias.
5. Click OK.
6. Repeat this process until you have added every computer on your LAN.
7. Click the **DNS** tab.
8. Type the IP address of the computers that serve as your Primary and Secondary DNS servers. You get these IP addresses from your ISP or, if you created your own DNS server, you can enter that server's IP address.
9. Type the name of the domain (probably the name of your local domain) to be searched for host names into the DNS Search Path box.
10. Click File → Save to save the changes.
11. Click File → Quit to exit.

Now, when you use programs such as `ftp`, `ssh`, or other TCP/IP utilities, you can use any host name that is identified on your local computer, exists in your search path domain, or can be resolved from the public Internet DNS servers. (Strictly speaking, you don't have to set up your `/etc/hosts` file. You could use IP addresses as arguments to TCP/IP commands, but names are easier to work with.)

## Adding Windows computers to your LAN

It is likely that you have other types of computers on your LAN in addition to those running Linux systems (at least for a few more years). If there is a DHCP server available on your LAN (or if you have configured one yourself as described in Chapter 23), Windows and most other computer systems can simply start up and begin using the network. In cases where your network card is not properly detected, or you want to set static IP addresses, you need to do some extra configuration.

The following are general steps for doing some manual steps to add your Windows computers to the Ethernet LAN you just created:

1. Power down your computer and install an Ethernet card. (Most PC Ethernet cards will run on Windows.)
2. Connect an Ethernet cable from the card to your hub.
3. Reboot your computer. If your card is detected, Windows will either automatically install a driver or ask you to insert a disk that comes with the card to install the driver.
4. Open the window to configure networking. (Start → Settings → Control Panel; then double-click the Network icon. If you have Windows XP, you also need to click "Set up or change your Internet connection..".) A window to change network properties appears.
5. What you do next depends on the version of Windows you are running:

   *For Windows 98:*
   - Find the Ethernet card you have just installed in the list and select it.
