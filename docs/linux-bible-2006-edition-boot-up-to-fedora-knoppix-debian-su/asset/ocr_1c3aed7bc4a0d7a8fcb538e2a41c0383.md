# Chapter 12 ♦ Running Yellow Dog Linux 375

On this screen, you also specify whether SELinux (Security-Enhanced Linux) policies activated on your system. These access control policies provide a much richer and more powerful environment for defining the access that users and applications can have to various resources.

10. Identify your network settings, including DHCP. You use your network configuration for LAN (local area network) connections, such as when you are using a router between your cable or DSL connection and the local, internal network. You should know these settings ahead of time, so be sure to check them out before you start.

Refer to Chapter 5 for descriptions of IP addresses, masks, and other information you need to set up your LAN.

If you are not prompted for network configuration information at this point, the installer could not identify your network card. This is extremely rare, but can happen with older Macs. If this occurs, contact Yellow Dog support for help in resolving this problem.

> Note

Select eth0 (your first network card) and click Edit. You have the following options:

+   **Configure DHCP** — Enables you to automatically obtain a DHCP address from your LAN if there is a DHCP server (such as Linksys or D-Link Routers). If you check here you do not need to fill out anything in this section.

+   **Activate on boot** — Enables you to join your network connection booting. Under most circumstances you will need to do so if you are using a LAN.

+   **IP Address** — A four-octet number that uniquely identifies your computer address. A class A network is 255.0.0.0, a class B is 255.255.0.0, and a class C is 255.255.255.0 by default (if no subnet masking is in place).

+   **Netmask** — Identifies the Host and network portions of the IP address.

Click OK, and if you aren't using DHCP, set your hostname by selecting Hostname: Manually. This can be any name you want to represent your computer. If this is a server, follow your company's naming convention. If you prefer to have DHCP set, select the Automatically DHCP radio button.

The last options are grayed out if you have selected DHCP. If you chose to manually configure your network options, enter the following:

+   **Gateway IP address** — The IP address of the machine that is the gateway or router between your network and the outside networks. For instance,