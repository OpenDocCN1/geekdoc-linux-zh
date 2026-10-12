# Other Uses for DHCP

A whole host of options can be used in **dhcpd.conf**: Entire books are dedicated to DHCP. The most comprehensive book is *The DHCP Handbook*, available at http://www.dhcp-handbook.com/. You can define NIS domains, configure NETBIOS, set subnet masks, and define time servers, or many other types of servers—to name a few of the DHCP options you can use. The preceding example will get your DHCP server and client up and running.

The DHCP server distribution contains an example of the **dhcpd.conf** file that you can use as a template for your network. The file shows a basic configuration that can get you started with explanations for the options used.

# Wireless Networking

As stated earlier, Linux has had support for wireless networking since the first standards were developed in the early 1990s. With computers getting smaller and smaller, the uses for wireless networking increased; meanwhile, the transmission speeds are increasing all the time. There are several different ways to create a wireless network. The following sections introduce you to several Linux commands you can use to initialize, configure, and manage wireless networking on your Fedora system.

# Support for Wireless Networking in Fedora

The Linux kernel that ships with Fedora provides extensive support for wireless networking. Related wireless tools for configuring, managing, or displaying information about a wireless connection include

+   *   **iwconfig**—Sets the network name, encryption, transmission rate, and other features of a wireless network interface

+   *   **iwlist**—Displays information about a wireless interface, such as rate, power level, or frequency used

+   *   **iwpriv**—Uses i to set optional features, such as roaming, of a wireless network interface

+   *   **iwspy**—Shows wireless statistics of a number of nodes

Support varies for wireless devices—most likely in the form of a PCMCIA adapter—although some USB wireless devices now work with Linux. In general, Linux wireless device software (usually in the form of a kernel module) supports the creation of an ether- net device that can be managed by traditional interface tools such as **ifconfig**—with wireless features of the device managed by the various wireless software tools.

For example, when a wireless networking device is first recognized and initialized for use, the driver will most likely report a new device: