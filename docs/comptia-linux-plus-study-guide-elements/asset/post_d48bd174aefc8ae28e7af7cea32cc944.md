
## Making Permanent Changes in Fedora

In Fedora, `etc/sysconfig/network-scripts/ifcfg-eth0` controls most network settings. (The filename varies depending on the network interface.) Listing 8.1 shows a typical `ifcfg-eth0` file, configured to use a static IP address.

### Listing 8.1: A Sample Fedora Network Configuration File

```text
DEVICE=eth0
BOOTPROTO=static
IPADDR=192.168.29.39
NETMASK=255.255.255.0
NETWORK=192.168.29.0
BROADCAST=192.168.29.255
GATEWAY=192.168.29.1
ONBOOT=yes
```

Several specific items are required, or at least helpful, for static IP address configuration:

- **IP address** You can set the IP address manually via the `ifconfig` command (described in more detail shortly) or via the IPADDR item in the configuration file.
- **Network mask** The netmask can be set manually via the `ifconfig` command or via the NETMASK item in a configuration file.
- **Gateway address** You can manually set the gateway via the `route` command. To set it permanently, you need to adjust a configuration file, which may be the same configuration file that holds other options or another file, such as `/etc/sysconfig/network/routes`. In either case, the option is likely to be called GATEWAY or gateway. The gateway isn’t necessary on a system that isn’t connected to a wider network—that is, if the system works *only* on a local network that contains no routers.

The network configuration script may hold additional options, but most of these are related to others. For instance, Listing 8.1 has an option specifying the interface name (`DEVICE=eth0`), another that tells the computer to assign a static IP address (`BOOTPROTO=static`), and a third to bring up the interface when the computer boots (`ONBOOT=yes`). The NETWORK and BROADCAST items in Listing 8.1 are derived from the IPADDR and NETMASK items, but you can change them if you understand the consequences.

## Making Permanent Changes in Ubuntu

Ubuntu Linux uses the `/etc/network/interfaces` file to hold IP address, netmask, and gateway information for all its interfaces. Listing 8.2 presents an example of this file.

### Listing 8.2: A Sample Ubuntu Network Configuration File

```text
# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
auto eth0
iface eth0 inet static
address 192.168.29.39
netmask 255.255.255.0
gateway 192.168.29.1
```

The loopback interface configuration in the first few lines of the file should never be touched. The eth0 configuration, though, can be altered to suit your needs. The entry includes the same basic information as appears in a Fedora configuration file, but the exact keywords and formatting differ. Also, pay attention to the line beginning with the keyword iface: it concludes with the word static. In a DHCP configuration, as noted earlier, it would end with dhcp, and the following address, netmask, and gateway lines would be absent.

## Setting DNS Options

In order for Linux to use DNS to translate between IP addresses and hostnames, you must specify at least one DNS server in the /etc/resolv.conf file. Precede the IP address of the DNS server by the keyword nameserver. You may include up to three such lines, although just one may be sufficient. (More than one provides redundancy in case the first name server becomes unresponsive.) This file may also include a domain keyword, which sets the Internet domain name in which the system resides, and one or more search keywords, which are additional domains that are searched if none is specified. For instance, to enable you to contact dino, pangaea.edu by using the shortened hostname dino, you could include the line search pangaea.edu, whether or not your computer is in the pangaea.edu domain. Listing 8.3 shows a sample resolv.conf file.

### Listing 8.3: A Sample /etc/resolv.conf File

```text
domain pangaea.edu
search luna.edu
nameserver 192.168.29.11
nameserver 172.24.24.24
nameserver 10.103.9.41
```

Adjusting this file is all you need to do to set the name server addresses; you don't have to do anything else to make the setting permanent. You might notice that Listing 8.3 specifies name servers on three different networks. This is perfectly valid (although for example purposes I've used addresses on reserved private networks). In general, though, the closer a DNS server is to your own system, the better.

> If you use DHCP, the DHCP client alters /etc/resolv.conf. Thus, if you make changes to this file and then use DHCP, your changes will be lost.

## Implementing Permanent Changes

If you’ve made manual changes to your configuration files, you can implement those changes by using the **ifup** and **ifdown** commands. These tools bring up or shut down a network interface, respectively, using the definitions in your configuration files. For instance, suppose you want to make changes to an existing configuration for eth0. Before making your changes, you would bring the interface down:

```bash
# ifdown eth0
```

After making your changes, you would bring it up:

```bash
# ifup eth0
```

The alternative to using these tools is to issue **ifconfig** and **route** commands to duplicate your changes, as described in the next section, “Setting Temporary Options.” Using **ifup** and **ifdown** is simpler and enables you to verify that your changes work the way you expect. Using the underlying **ifconfig** and **route** commands is better for making temporary changes, such as adding a notebook computer to a hotel network to which it will be connected only briefly.

## Setting Temporary Options

As mentioned earlier, the **ifconfig** program is critically important for setting both the IP address and netmask. This program can also display current settings. Basic use of **ifconfig** to bring up a network interface resembles the following:

```bash
ifconfig interface up addr netmask mask
```

For instance, the following command brings up eth0 (the first Ethernet card) using the address 192.168.29.39 and the netmask 255.255.255.0:

```bash
# ifconfig eth0 up 192.168.29.39 netmask 255.255.255.0
```

This command links the specified IP address to the card so that the computer will respond to the address and claim to be that address when sending data. It doesn’t, though, set up a route for traffic beyond your current network. For that, you need to use the **route** command:

```bash
# route add default gw 192.168.29.1
```

Substitute your own gateway address for 192.168.29.1. (Advanced routing and the **route** command are described in more detail in Chapter 9.) Both **ifconfig** and **route** can display information on the current network configuration. For **ifconfig**, omit up and everything that follows; for **route**, omit add and everything that follows. For instance, to view interface configuration, you might issue the following command:

```bash
# ifconfig eth0
eth0  Link encap:Ethernet  HWaddr 00:A0:CC:24:BA:02
inet addr:192.168.29.39  Bcast:192.168.29.255  Mask:255.255.255.0
UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
RX packets:10469 errors:0 dropped:0 overruns:0 frame:0
TX packets:8557 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:100
RX bytes:1017326 (993.4 Kb)  TX bytes:1084384 (1.0 Mb)
Interrupt:10 Base address:0xc800
```

When configured properly, ifconfig should show a hardware address (HWaddr), an IP address (inet_addr), and additional statistics. There should be few or no errors, dropped packets, or overruns for both received (RX) and transmitted (TX) packets. Ideally, few (if any) collisions should occur, but some are unavoidable if your network uses a hub rather than a switch. If collisions total more than a few percent of the total transmitted and received packets, you may want to consider replacing a hub with a switch. To use route for diagnostic purposes, you might try the following:

```bash
# route
Kernel IP routing table
Destination    Gateway         Genmask         Flags Metric Ref    Use Iface
192.168.29.0   *               255.255.255.0   U     0       0      0  eth0
127.0.0.0      *               255.0.0.0       U     0       0      0  lo
default        192.168.29.1    0.0.0.0         UG    0       0      0  eth0
```

This shows that data destined for 192.168.29.0 (that is, any computer with an IP address between 192.168.29.1 and 192.168.29.254) goes directly over eth0. The 127.0.0.0 network is a special interface that “loops back” to the originating computer. Linux uses this for some internal networking purposes. The last line shows the default route—everything that doesn’t match any other entry in the routing table. This line specifies the default route’s gateway system as 192.168.29.1. If it’s missing or misconfigured, some or all traffic destined for external networks, such as the Internet, won’t make it beyond your local network segment.

As with DHCP configuration, it’s almost always easier to use a GUI configuration tool to set up static IP addresses, at least for new administrators. The exact locations of the configuration files differ from one distribution to another, so the examples listed earlier may not apply to your system.

## Using GUI Configuration Tools

Most distributions include their own GUI configuration tools for network interfaces. For instance, Fedora and Red Hat ship with a custom GUI tool called Network Configuration (system-config-network-gui) and a text-mode tool called system-config-network-tui. SUSE has a text-mode and GUI tool called YaST, and Ubuntu ships with a GUI tool called Network Settings (network-admin). The details of operating these programs differ, but the GUI configuration tool provides a means to enter the information described earlier.
