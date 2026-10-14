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

Some systems have two or more physical network devices. For example, you might have two Ethernet cards, or an Ethernet card and a DSL Internet connection. By having two devices, you can connect to two networks at the same time. This illustrates the purpose of a gateway: packets arriving at the gateway computer via one of the network devices need to leave the computer via the other network device in order to reach their intended destination. To