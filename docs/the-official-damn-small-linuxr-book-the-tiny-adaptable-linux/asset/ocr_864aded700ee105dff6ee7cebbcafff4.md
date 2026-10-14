dialup session. When you see an IP number, the communication link is established and you may begin to use the Internet applications included with DSL.

# Ethernet Configuration

Wired and wireless Ethernet connections are supported in DSL. If you cannot automatically connect to a network, the following sections help you to configure an Ethernet connection manually.

# Wired Options

Because DSL boots with an automatic DHCP request, often nothing is required to have immediate network access. For those users who have more demanding needs, DSL offers the Netcardconfig program. To access this program, from the DSL Control Panel, select Netcardconfig; or from the system menu, select System, Net Setup, Netcardconfig.

Step through the questions as they are presented. If you are connected to a device or LAN with an available DHCP server, you can select Yes and probably be connected to the Internet. If you can’t detect the DHCP server or need to configure your addresses manually, select No. Then you will be expected to enter a static IP address, netmask, broadcast address, default gateway, and DNS nameservers. If you don’t know what that information is, contact your Internet Service Provider for assistance.

# Wireless

Wireless network access is something that cannot be initially automatically set up because of the requirement of a network access point and encryption key. You should always boot your system with the nodhcp boot option. Having DSL try to connect to a DHCP server could block you from manually setting up your wireless connection, so nodhcp prevents that from happening.

All DSL wireless setup attempts are automatically detected upon a normal shutdown. You are prompted to save your wireless setup. Each custom GUI creates a script of your wireless setup information. These scripts can be found in the /opt directory.

Many older wireless cards work with the Iwconfig, Prism2 config, or Wlanconfig tools. For later wireless cards, however, for which open source drivers are not yet available, you may need to use Ndiswrapper, which lets you provide a wireless card’s Windows driver to get the card to work in Linux.