
As you work with more complex networks than those described so far, you'll find it helpful to be familiar with the output and the options of the route command. At times you may need to modify or add routes to make your Linux system function as desired within a larger network that has multiple gateways or uses network prefixes that require manual configuration.

Recall that you normally use the service command to start or stop networking, and that this command relies on the script /etc/rc.d/init.d/network. This script, in turn, relies on information stored in the file /etc/sysconfig/network and the files located in the directories /etc/sysconfig/network-scripts and /etc/sysconfig/networking/devices. Within the latter directory, you see a file for each network device, such as ifcfg-eth0. The contents of the ifcfg-eth0 file might look like this:

```
# 3Com Corporation |3c905B 100BaseTX [Cyclone]
DEVICE=eth0
BOOTPROTO=none
BROADCAST=192.168.100.255
HWADDR=00:01:02:76:FA:79
IPADDR=192.168.100.25
NETMASK=255.255.255.0
NETWORK=192.168.100.0
ONBOOT=yes
TYPE=Ethernet
DHCP_HOSTNAME=inverness.xmission.com
USERCTL=no
PEERDNS=no
```

![](img/43f64015de86d989e30eff5bb284fb96_553_0.png)

If you are using DHCP to obtain IP address information, your ifcfg-eth0 file will look different from the one shown here.

The contents of all of these files are used by the /etc/rc.d/init.d/network script as it executes ifconfig and route commands. To change the IP address or other networking parameters for your computer, you can simply change the information in /etc/sysconfig/network-scripts/ifcfg-eth0 and then execute this command:

```
# service network restart
```

![](img/43f64015de86d989e30eff5bb284fb96_553_1.png)

You should not make haphazard changes in your networking. They might not only stop your system from working, but can interfere with other users' systems.

If you want to manage a single interface rather than all network interfaces that are configured on the system, you can use the ifup and ifdown scripts instead of the service command. These two scripts are located in the directory /etc/sysconfig/network-scripts. You can use these scripts to "bring up" or "take down" a specific network interface, without affecting other interfaces. Using one of these scripts is generally better than using the ifconfig command directly, because the scripts can carefully look at all the parameters and associated functionality needed to cleanly manage the interface. As an example, you can stop the Ethernet interface, eth0, using this command (assuming you are in the directory /etc/sysconfig/network-scripts):

```
# ./ifdown eth0
```

After making modifications to the Ethernet configuration, you can start the interface again using this command:

```
# ./ifup eth0
```

Normally, only the root account can use the network configuration commands and scripts. You can modify the USERCTL field in the device files, however, so that a regular user can start or stop a network interface using the service, ifup, or ifdown command. You can also configure this feature using the graphical utility described in the next section.

To see the flexibility and usefulness of this system and its many scripts and configuration files, consider how you would manually add a new interface. Suppose that you needed to assign a second IP address to your Ethernet card. This is called IP aliasing, when a single physical interface has more than one IP address assigned—a feature that is useful when hosting multiple Web sites on a single machine, for example. IP aliases are referred to by adding a number to the physical interface name. So, if the interface is eth0, the first additional IP address would refer to eth0:1, the second to eth0:2, and so on.

To create the IP alias you need, you simply create a new file in the /etc/sysconfig/network-scripts directory with the name ifcfg-eth0:1. The easiest way is to copy the existing file ifcfg-eth0. Then change the values of the DEVICE and IPADDR lines to refer to eth0:1 and the second IP address you wanted to assign to the Ethernet card. Then you restart networking to make the additional IP address automatically active. Every time you start up Linux, the additional IP address is started. To remove this IP alias, you just delete the additional file that you created and restart networking. You experiment with creating an IP alias in the Hands-On Projects at the end of the chapter.

Some systems have two or more physical network devices. For example, you might have two Ethernet cards, or an Ethernet card and a DSL Internet connection. By having two devices, you can connect to two networks at the same time. This illustrates the purpose of a gateway: packets arriving at the gateway computer via one of the network devices need to leave the computer via the other network device in order to reach their intended destination. To permit this, you must enable IP forwarding. IP forwarding is a feature of the Linux kernel that allows packets to be passed between network interfaces. IP forwarding is required for any router. To enable IP forwarding, you use this command:

```
# echo 1 > /proc/sys/net/ipv4/ip_forward
```

## Configuring Networking Using Graphical Tools

A good system administrator knows how things work "under the hood," rather than just relying on graphical tools. By knowing about the networking scripts and the ifconfig and route commands, you'll have a better grasp of how to diagnose any problems that arise on your network. Once you understand those things, however, there's no reason not to use the tools that make life easier. Every major version of Linux includes graphical utilities to help you set up and manage networking.

Red Hat Linux and Fedora include the system-config-network program. You can start this program from the command line or by choosing System Settings, then Network on the GNOME main menu. Figure 12-1 shows the Devices tab of this utility. As the text in the tab notes, multiple Linux networking devices can be associated with a single physical piece of hardware.

![](img/43f64015de86d989e30eff5bb284fb96_555_0.png)

Figure 12-1 The Devices tab of system-config-network

> NOTE
> This section discusses only the Hardware and Devices tabs. The Hosts and DNS tabs are discussed later in this chapter.

On the Devices tab, you see a list of each Linux networking device name and the type of hardware driver associated with it. You can use the New button in the top section of the dialog box to configure many types of networking interfaces, though not nearly as many as Linux actually supports. Figure 12-2 shows the dialog box that walks you through creating a new device after you click New.

![](img/43f64015de86d989e30eff5bb284fb96_556_0.png)

Figure 12-2 Beginning to create a new device in system-config-network

You can easily use this tool to set up IP aliasing, adding another IP address to a single Ethernet card. Just select Ethernet as the device type, then select the same Ethernet card in the second dialog box. When prompted to enter address information, enter the new (second) IP address. (See Figure 12-3.) The utility automatically assigns it an appropriate device name (such as eth0:1), which you see in the Devices tab when you complete the configuration.

If you select an existing device and click Edit, you can view and alter the configuration of that device. Figure 12-4 shows the dialog box that appears when you select an Ethernet device and click Edit. The General tab lets you decide whether to use DHCP to obtain an IP address or assign a static IP address. You can also define whether regular users can activate the networking device, whether the device should be started at boot time, and which parts of the configuration are provided by DHCP (DNS server, host name, or just an IP address).

![](img/43f64015de86d989e30eff5bb284fb96_557_0.png)

Figure 12-3 An IP alias's Ethernet device

![](img/43f64015de86d989e30eff5bb284fb96_557_1.png)

Figure 12-4 Editing an Ethernet device in system-config-network
