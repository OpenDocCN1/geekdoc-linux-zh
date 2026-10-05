
# Solaris firewalls and filtering

variables. Many variable names are the same, so you can partially work around Sun's minimal **ndd** man page.

Interface-specific options such as link speed, autonegotiation, and jumbo packet support are also set with **ndd**; run **ndd** directly on the device file for the interface (e.g., `/dev/e100g0`). Unfortunately, the way Sun has set this up nowadays makes the names of the configuration parameters dependent on the specific driver, so it isn't a universal recipe for it, locking a network interface to 100 Mb/s.

To change speeds, you'll need to identify the writable "capability" variables for speed (usually named `_cap`) and turn off (set to zero) all the ones you want to disallow. Turn off the `_autoneg_cap` variable, to disable autonegotiation. For example, the following script sets `/dev/e100g0` to 100 Mb/s full duplex on one of our machines:

```sh
#!/bin/sh
ndd -dev/e100g0 adv_autoneg_cap 0
ndd -dev/e100g0 adv_1000fdx_cap 0
ndd -dev/e100g0 adv_100fdx_cap 1
ndd -dev/e100g0 adv_10hdx_cap 0
ndd -dev/e100g0 adv_10fdx_cap 0
ndd -dev/e100g0 adv_10hdx_cap 0
```

# Solaris security

Table 14.11 shows Solaris's default behavior with regard to very touchy network issues. For a brief description of the implications of these behaviors, see Security issues starting on page 472. You can adjust most of these using **ndd**.

| Feature | Default | ndd variable |
| :--- | :--- | :--- |
| IP forwarding | off | ip_forwarding |
| ICMP redirects | obeys | Can't be changed* |
| Routing source | ignores | ip_forward_src_routed |
| Broadcast ping (respond) | on | ip_respond_to_echo_broadcast |
| Broadcast ping (forward) | off | ip_forward_directed_broadcasts |

a. You can only modify the entries' time-to-live.

# Solaris firewalls and filtering

As mentioned in the **Security issues section**, you generally shouldn't use a UNIX, Linux, or Windows box as a firewall or NAT gateway. A dedicated piece of network hardware stands. Solaris used to make it easy to follow this rule by including any filtering software, but Darren Reed's free IPFilter software has now been bundled into the basic distribution. If you must use a UNIX-based filter, this is a good choice—it was always our favorite of the add-on filters for Solaris.

# Chapter 14 TCP/IP Networking

The IPFilter suite implements IP filtering, NAT, and transparent packet forwarding. It is free, open source, and works on either SPARC or Intel hardware. The IPFilter package includes **ipf** for configuring a firewall, **ipstat** for outputting the filtering rules that have been installed, and **ipnat** for implementing NAT.

See Chapter 22, *Security*, for details on packet filtering with IPFilter. The section about this topic starts on page 939. Here, we discuss only IPFilter's NAT features.

# Solaris NAT

To make NAT work, you must tell the kernel what addresses to map from, what addresses to map, and what port range to extend the address space. See page 462 for a general discussion of NAT and the mechanisms it uses to bridge from private to public address space.

To configure NAT, you supply rules to the **ipnat** command. The rules are similar to those used with **ipf** to implement packet filtering. But beware: like **ipf** rules are ordered. However, they have opposite precedence. To keep on your toes, the *first* matching rule is selected, not the last.

Below are examples of **ipnat** rules. To be activated at boot time, these would go in the **/etc/ipf/ipnat.conf** file:

```
eth1 192.168.1.0/24 -> 128.138.198.0/26 portmap tcp/udp 20000:65000
eth1 192.168.1.0/24 -> 128.138.198.0/26
```

We have assumed that eth1 is our interface to the Internet and that our internal network is numbered with class C. These rules map addresses from a /24 network into addresses from a /26 network can accommodate only one-quarter of the hosts. The *portmap* clause extends the address range by allowing each address to use. The first rule covers all TCP and UDP traffic but does not affect ICMP; the second rule catches ICMP messages and tries to get them back to the right host. If the kernel cannot unambiguously determine who should receive a particular ICMP message, the packet goes out as a broadcast; machines that receive it out of context can ignore it. On a home machine, you might be assigned a real IP address by your ISP's DHCP server. If you are given a static address assignment, give the target network in the *map* line designation and a large port range to accommodate the needs of all local hosts. If you get a dynamically address each time you connect, use the notation 0/32 in the *map* line; it will make **ipnat** read the address directly from the network interface. For example, here is a line you might use for a single, dynamically assigned address:

```
eth1 192.168.1.0/24 -> 0/32 portmap tcp/udp 20000:65000
```

# Solaris networking quirks

To test the configuration, delete all existing rules.

The output of ifconfig -a is different when run as a regular user than when run as root; it shows the link-level Ethernet addresses in addition to the IP addresses. Solaris lets you change the link-level (MAC) address of a network interface with the ifconfig command. This feature can be useful if you need to grow your way onto a restricted network.

# HP-UX Networking

HP-UX network configuration is easy: all configuration parameters are set in the file /etc/rc.config.d. The values in this file (and other files in the directory) are loaded into the environment at boot time and used by the /sbin/rc script as the machine boots. netconf is liberally scattered with comments that tell you which variables must be set and what they mean.

# Basic network configuration for HP-UX

To assign a hostname to a machine and configure its first interface, the netconf file and assign a value to the following variables:

```
HOSTNAME
INTERFACE_NAME
IP_ADDRESS
BNET_MASK
```

For example:

```
HOSTNAME=lan0
INTERFACE_NAME=192.168.1.99
IP_ADDRESS=255.255.255.0
```

A second network interface would subscribe 1, and its existence would be indicated by the variable NET_CARDS set to 2. The netconf file also contains variables to configure static routes and start a restarting daemon. To establish a default route, set the following variables:

```
ROUTE_DESTINATION=default
ROUTE_MASK=""
ROUTE_GATEWAY=192.168.21.254
ROUTE_COUNT=1
```

# TCP/IP Networking

The ROUTE_MASK variable is needed for a network in which the netmask differs from the default for the class of addresses used. The ROUTE_COUNT variable should be 0 if the gateway is the local machine and 1 if it is remote. To add more static routes, just enter their parameters to a set of ROUTE_ variables [1], [2], etc. These arguments are passed directly to the route command. For example, the destination parameter can be the word default as not netaddr or hostaddr.

HP-UX supplies gated but not routed; to use gated, the variable GATED and GATED_ARGS to the arguments you wanted. See Chapter 15, Routing, for bit more information about gated. The HP-UX man on routing (man routing) contains a lot of background information.

Many fields in the netconf file contain either a hostname or an IP address. If a hostname is used, it must be defined in /etc/hosts. At boot time, HP-UX looks at /etc/hosts and does not use any other name lookup mechanism. The machines in /etc/hosts should have their fully qualified domain names listed first, followed by their short names and all aliases.

HP uses the ifconfig command to show information about the network interfaces on a machine. if ifconfig does not work, ifconfig does. Network interface names begin with "lan" or "snap": lan for Ethernet link-layer encapsulation and snap for IEEE 802.3 encapsulation. The first interface is lan0, the second is lan1, and so on.

HP-UX has the same sort of "plumbing" concept as Solaris does, but interfaces are automatically plumbed when they are assigned an IP address by ifconfig.

SMH is HP's system administration tool, which is aligned to make UNIX system administration a breeze. It is a menu-based system and can be used to configure network interfaces, as well as to perform many other sysadmin chores.

# HP-UX configuration examples

To bring up an HP-UX network interface and add a default route by hand, you'd use sudo commands as the following:

```
hp-ux$ sudo ifconfig lan 192.168.21.99 netmask 0xffffff
hp-ux$ sudo route add default 192.168.21.254 1
```
