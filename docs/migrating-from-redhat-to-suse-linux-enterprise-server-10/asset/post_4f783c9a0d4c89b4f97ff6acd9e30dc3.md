
If you run this command as a user other than root, you must enter the absolute path to the command (`sbin/ip`).

3-12 Copying all or part of this manual, or distributing such copies, is strictly prohibited. To report suspected copying, please call 1-800-PIRATES. Version 1

### Exercise 3-1 Manage the Network Configuration Information from YaST

Up to now, your system got all network configuration information via DHCP. In this exercise you change all the important information into static values.

You will find this exercise in the workbook.

*(End of Exercise)*

Although almost every step of a network configuration is done for you when you use YaST, it’s sometimes useful to configure the network settings manually. For testing and troubleshooting, it can be much faster to change the network setup from the command line.

In this section, you learn how to configure network devices manually. You also learn how to configure routing with command line tools and how to save the network setup to configuration files.

- Set Up Network Interfaces with the ip Tool
- Set Up Routing with the ip Tool

## Set Up Network Interfaces with the ip Tool

You normally configure a network card with YaST during or after installation. You can use the tool **ip** to change the network interface configuration quickly from the command line.

The command **ip** is available on RHEL as well as on SUSE Linux Enterprise Server 10.

Changing the network interface configuration at the command line is especially useful for testing purposes; if you want a configuration to be permanent, you must save it in a configuration file. These configuration files are generated automatically when you set up a network card with YaST.

You can use **ip** to perform the following tasks:

- Display the Current Network Configuration
- Change the Current Network Configuration

> You can enter `/sbin/ip` as a normal user to display the current network setup only. To change the network setup, you have to be logged in as root.

As changes made with `ip` are lost with the next reboot, you also have to know how to:

- Save Device Settings to a Configuration File

## Display the Current Network Configuration

With the `ip` tool, you can display the following information:

- IP Address Setup
- Device Attributes
- Device Statistics

### IP Address Setup

To display the IP address setup of all interfaces, enter `ip address show`. Depending on your network setup, you see information similar to the following:

```
da2:~ # ip address show
1: lo: <LOOPBACK,UP> mtu 16436 qdisc noqueue
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 brd 127.255.255.255 scope host lo
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,NOARP> mtu 1500 qdisc pfifo_fast qlen 1000
    link/ether 00:30:05:4b:98:85 brd ff:ff:ff:ff:ff:ff
    inet 10.0.0.2/24 brd 10.0.0.255 scope global eth0
    inet6 fe80::230:5ff:fe4b:9885/64 scope link
       valid_lft forever preferred_lft forever
3: sit0: <NOARP> mtu 1480 qdisc noqueue
    link/sit 0.0.0.0 brd 0.0.0.0
```

The information is grouped by network interfaces. Every interface entry starts with a digit, called the *interface index*, with the interface name displayed after the interface index.

In the above example, there are 3 interfaces:

- **lo.** The loopback device, which is available on every Linux system, even when no network adapter is installed. (As stated above, “device” and “interface” are often used synonymously in the context of network configuration.) Using this virtual device, applications on the same machine can use the network to communicate with each other.
  - For example, you can use the IP address of the loopback device to access a locally installed web server by typing [http://127.0.0.1](http://127.0.0.1) in the address bar of your web browser.
- **eth0.** The first Ethernet adapter of the computer in this example. Ethernet devices are normally called eth0, eth1, eth2, and so on.
- **sit0.** This is a special virtual device which can be used to encapsulate IPv4 into IPv6 packets. It’s not used in a normal IPv4 network.

You always have the entries for the loopback and sit devices. Depending on your hardware setup, you might have more Ethernet devices in the `ip` output.

Several lines of information are displayed for every network interface, such as `eth0` in the preceding example:

```
2: eth0: <BROADCAST,MULTICAST,NOTRAILERS,UP> mtu 1500 qdisc pfifo_fast qlen 1000
```

The most important information of the line in this example is the interface index (2) and the interface name (eth0).

The other information shows additional attributes set for this device, such as the hardware address of the Ethernet adapter (00:30:05:4b:98:85):

```
link/ether 00:30:05:4b:98:85 brd ff:ff:ff:ff:ff:ff
```

In the following line, the IPv4 setup of the device is displayed:

```
inet 10.0.0.2/24 brd 10.0.0.255 scope global eth0
```

The IP address (10.0.0.2) follows `inet`, and the broadcast address (10.0.0.255) after `brd`. The length of the network mask is displayed after the IP address, separated by a `/`. The length is displayed in bits (24).

The following lines show the IPv6 configuration of the device:

```
inet6 fe80::230:5ff:fe4b:9885/64 scope link
   valid_lft forever preferred_lft forever
```

The address shown here is automatically assigned, even though IPv6 is not used in the network that is connected with the device. The address is generated from the hardware address of the device.

Depending on the device type, the information can differ. However, the most important information (such as assigned IP addresses) is always shown.

### Device Attributes

If you are only interested in the device attributes and not in the IP address setup, you can enter `ip link show`:

```
da2:~ # ip link show
1: lo: <LOOPBACK,UP> mtu 16436 qdisc noqueue
   link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: eth0: <BROADCAST,MULTICAST,NOTRAILERS,UP> mtu 1500 qdisc pfifo_fast qlen 1000
   link/ether 00:30:05:4b:98:85 brd ff:ff:ff:ff:ff:ff
3: sit0: <NOARP> mtu 1480 qdisc noqueue
   link/sit 0.0.0.0 brd 0.0.0.0
```

The information is similar to what you have seen when entering **ip address show**, but the information about the address setup is missing. The device attributes are displayed in brackets right after the device name.

The following is a list of possible attributes and their meanings:

- **UP**. The device is turned on. It is ready to accept packets for transmission and it’s ready to receive packets from the network.
- **LOOPBACK**. The device is a loopback device.
- **BROADCAST**. The device can send packets to all hosts sharing the same network.
- **POINTTOPOINT**. The device is only connected to one other device. All packets are sent to and received from the other device.
- **MULTICAST**. The device can send packets to a group of other systems at the same time.
- **PROMISC**. The device listens to all packets on the network, not only to those sent to the device’s hardware address. This is usually used for network monitoring.

### Device Statistics

You can use the option **-s** with the command **ip** to display additional statistics information about the devices. The command looks like the following:

```
ip -s link show eth0
```

By giving the device name at the end of the command line, the output is limited to one specific device. This can also be used to display the address setup or the device attributes.

The following is an example of the information displayed for the device `eth0`:

```
da2: # ip -s link show eth0
2: eth0: <BROADCAST,MULTICAST,NOTRAILERS,UP> mtu 1500 qdisc pfifo_fast qlen 1000
    link/ether 00:30:05:4b:98:85 brd ff:ff:ff:ff:ff:ff
RX:  bytes packets errors dropped overrun mcast
     849172787 9304150 0 0 0 0
TX:  bytes packets errors dropped carrier collisions
     875278145 1125639 0 0 0 0
```

Two additional sections with information are displayed for every device. Each of the sections has a headline with a description of the displayed information.

The section starting with `RX` displays information about received packets, and the section starting with `TX` displays information about sent packets.

The sections display the following information:

- **Bytes.** The total number of bytes received or transmitted by the device.
- **Packets.** The total number of packets received or transmitted by the device.
- **Errors.** The total number of receiver or transmitter errors.
- **Dropped.** The total number of packets dropped due to a lack of resources.
- **Overrun.** The total number of receiver overruns resulting in dropped packets.
  - As a rule, if a device is overrun, it means that there are serious problems in the Linux kernel or that your computer is too slow for the device.
- **Mcast.** The total number of received multicast packets. This option is supported by only a few devices.
