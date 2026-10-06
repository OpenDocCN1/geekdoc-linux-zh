
# Understanding Configuration Files and Scripts

RHCE PREPARATION TOPICS COVERED IN THIS CHAPTER:

- Understand the role of the scripts and configuration files under /etc/sysconfig.
- Understand the role of the scripts and configuration files under /etc/sysconfig/network-scripts.
- Understand how Plug-and-Play cards, including sound cards, are configured.
- Understand the role and contents of /etc/inittab.
- Understand the role and contents of /etc/fstab.

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_369_0.png)

In addition to the AT&T SysV Unix-style start-up scripts, Red Hat Linux uses several other sets of scripts during system initialization. This chapter describes these scripts and explains how to use them to configure system start-up.

# The /etc/sysconfig Network Files and Scripts

When the /etc/rc.d/init.d/network network start-up script runs, it brings up the configured network interface devices. It does so by invoking a set of scripts stored in the /etc/sysconfig/network-scripts directory. Table 15.1 summarizes these scripts, which can perform a variety of operations besides bringing up network interfaces.

TABLE 15.1 Scripts in /etc/sysconfig/network-scripts

| Script | Description |
|---|---|
| chat-* | Chat scripts for PPP and SLIP connections |
| ifcfg-* | Stores the configuration of the associated interface; for example, ifcfg-eth0 stores the configuration of the first Ethernet card, and ifcfg-lo0 stores the configuration of the TCP/IP dummy loopback device |
| ifdhcp-done | Configures /etc/resolv.conf if DHCP is used |

TABLE 15.1 Scripts in /etc/sysconfig/network-scripts (continued)
| Script | Description |
| --- | --- |
| ifdown-* | Brings down the associated protocol; for example, ifdown-ppp brings down PPP |
| ifdown-post | Brings down a specified device |
| ifup-* | Brings up the associated protocol; for example, ifup-ppp brings up PPP |
| ifup-aliases | Adds IP aliases for a specified device |
| ifup-post | Brings up a specified device, adding static routes and aliases and setting the host name |
| ifup-routes | Adds static routes for a specified device |

## The ifcfg-* Scripts

Each ifcfg-* script stores the configuration for a network interface. The /sbin/ifup and /sbin/ifdown use these configuration scripts to bring up or bring down, respectively, an interface. For example, a system that has an Ethernet network interface will store the interface configuration in /etc/sysconfig/network-scripts/ifcfg-eth0; if the system has a second Ethernet network interface, the interface configuration will be stored in /etc/sysconfig/network-scripts/ifcfg-eth1, and so on. To bring the first Ethernet card, you can issue the command

/sbin/ifup ifcfg-eth0
or simply

/sbin/ifup eth0

The command supplies the ifcfg-prefix if you omit it.

Copyright © 2000 SYBEX, Inc., Alameda, CA www.sybex.com

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_371_0.png)

The ifup and ifdown scripts use the ifconfig command (described in a subsection below), which is a privileged command. Therefore, ordinary users cannot execute ifup and ifdown scripts, unless you specify that the associated interface is user controllable. Non-privileged users may require a simpler user interface than that provided by the ifup and ifdown scripts. Such users may prefer to use the usernet and userctl commands, which are available to them if the interface is user controllable. See the usernet and userctl man pages for details.

The ifcfg-* scripts contain commands that set the values of environment variables that specify the network configuration. For example, here’s a typical ifcfg-eth0 script:

```
DEVICE="eth0"
IPADDR="192.168.1.3"
NETMASK="255.255.255.0"
ONBOOT="yes"
BOOTPROTO="none"
```

If you use linuxconf to establish the network configuration, the file will contain statements that set a variety of IPX-related environment variables, even if your system is not configured for IPX. The example configuration corresponds to a static Ethernet configuration. It includes:

- The device name, DEVICE=eth0
- The IP address, IPADDR=192.168.1.3
- The network subnet mask, NETMASK=255.255.255.0
- A parameter indicating that the device should be started when the system boots, ONBOOT=yes
- A parameter indicating that the configuration is static, BOOTPROTO=none

A static Ethernet configuration may also include:

- A network address, NETWORK=192.168.1.0
- A network broadcast address, BROADCAST=192.168.1.255

If you configure an interface to obtain its configuration via DHCP, the contents of the file are somewhat different. It includes the following:

- The device name, DEVICE=eth0
- The boot protocol, BOOTPROTO=dhcp
- A parameter indicating that the device should be started when the system boots, ONBOOT=yes

You can revise the network configuration via linuxconf or netcfg, or you can modify the files using a text editor.

# The /etc/sysconfig/network Script

Global network configuration information affecting each interface is stored in /etc/sysconfig/network. Here's a typical /etc/sysconfig/network file.

```
NETWORK=yes
FORWARD_IPV4="yes"
HOSTNAME="athlon.azuspacific.com"
GATEWAY="192.168.1.1"
GATEWAYDEV="eth1"
```

The file indicates that networking is active and that the system will route packets. The host name of the system is athlon.azuspacific.com; its default gateway is 192.168.1.1, which is accessible via the Ethernet interface known as eth1. If the system uses NIS, the file would also indicate the NIS domain with which it's associated.

Now, complete Exercise 15.1, which asks you to study the networking configuration files.

## EXERCISE 15.1: Network Configuration Scripts

For the RHCE exam, it's important to know how to configure networking with and without the use of configuration utilities. To configure networking without configuration utilities, you must know the name and function of each network configuration file. To learn more about these files, inspect the network configuration files of a working Linux server. Verify that you understand the role and contents of each file. Now you can freely refer to this book and other documentation. Before taking the RHCE exam, be sure that you can find each file and explain its function without consulting any documentation.

# Network Administration Commands

Several commands help you administer networking. Among the most important are the following:

- ifconfig
- netstat
- arp

This section explains the operation of these.

## The ifconfig Command

The ifconfig command reports the status of a network interface and lets you add or remove an interface. It's run by the /etc/sysconfig/network-scripts.

## Reporting Interface Status

To obtain a report on the status of interfaces, issue the ifconfig command. The output of the command will resemble the following:

```
eth0 link encap:Ethernet hwaddr 00:53:68:A2:AE:EC
  inet addr:192.168.1.1  broadcast:192.168.1.255  netmask:255.255.255.0
  UP BROADCAST,MULTICAST  mtu:1500  metric:1
  packets=75545  errors=0  dropped=0  overrun=0  frame=0
  bytes=1234568(RX) collisions=0  compressed=0
```

```
eth1 link encap:Ethernet hwaddr 00:CC:25:8A:EC:30
  inet addr:192.168.1.2  broadcast:192.168.1.255  netmask:255.255.255.0
  UP BROADCAST,MULTICAST  mtu:1500  metric:1
  packets=123  errors=0  dropped=0  overrun=0  frame=0
  bytes=4567(TX) collisions=00=0
```

```
lo link encap:Local Loopback
  inet addr:127.0.0.1  netmask:255.255.0.0
  UP LOOPBACK,MULTICAST  mtu:1500  metric:1
  packets=75545  errors=0  dropped=0  overrun=0  frame=0
  bytes=1234568(RX) collisions=0
```

The example output shows two Ethernet cards, eth0 and eth1, plus the TCP/IP dummy lookup device, lo. Table 15.2 describes the fields included in the report.

TABLE 15.2 Fields in ifconfig Output

| Field | Description |
| --- | --- |
| Link encap | The type of interface |
| Haddr | The hardware address (MAC) of the interface |
| inet addr | The IP address of the interface |
| Bcast | The broadcast address for the network |
| Mask | The netmask for the subnet |
| Status | The interface status (for example, UP RUNNING MULTICAST) |
| MTU | The maximum transfer unit size (bytes) |
| Metric | The interface metric, which is used by some routing protocols |
