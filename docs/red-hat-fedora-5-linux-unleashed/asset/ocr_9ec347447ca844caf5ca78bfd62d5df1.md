# **NOTE**

DSL service is an "always-on" type of Internet service, although you can turn off the connection under Fedora using the Network Device Control. An always-on connection exposes your computer to malicious abuse from crackers who trawl the Internet attempting to gain access to other computer systems. In addition to the capability to turn off such connections, Fedora provides a firewall to keep crackers out; you configured a simple firewall during the original installation. The firewall can also be configured from the Security Level Configuration tool found in the System Settings menu selection as Security Level.

A DSL connection requires that you have an ethernet network interface card (sometimes a USB interface that is not easily supported in Linux) in your computer or notebook. Many users also configure a gateway, firewall, or other computer with at least two network interface cards in order to share a connection with a LAN. We looked at the hardware and protocol issues earlier in this chapter. Advanced configuration of a firewall or router, other than what was addressed during your initial installation of Fedora, is beyond the scope of this book.

# Understanding Point-to-Point Protocol over Ethernet

Establishing a DSL connection with an ISP providing a static IP address is easy. Unfortunately, many DSL providers use a type of PPP protocol named Point-to-Point Protocol over Ethernet (PPPoE) that provides dynamic IP address assignment and authentication by encapsulating PPP information inside ethernet frames. Roaring Penguin's rp-pppoe clients are included with Fedora, and these clients make the difficult-to-configure PPPoE connection much easier to deal with. You can download and install newer versions (see the Roaring Penguin link in the “Reference” section at the end of this chapter).

# Configuring a PPPoE Connection Manually

The basic steps involved in manually setting up a DSL connection using Fedora Core Linux involve connecting the proper hardware, and then running a simple configuration script if you use rp-pppoe from Roaring Penguin.

First, connect your DSL modem to your telephone line, and then plug in your ethernet cable from the modem to your computer's network interface card. If you plan to share your DSL connection with the rest of your LAN, you need at least two network cards—designated eth0 (for your LAN) and eth1 (for the DSL connection).

The following example assumes that you have more than one computer and will share your DSL connection on a LAN. First, log in as root, and ensure that your first eth0 device is enabled and up (perhaps using the ifconfig command). Next, bring up the other interface, but assign a null IP address like this:

```
# /sbin/ifconfig eth0 0.0.0.0 up
```