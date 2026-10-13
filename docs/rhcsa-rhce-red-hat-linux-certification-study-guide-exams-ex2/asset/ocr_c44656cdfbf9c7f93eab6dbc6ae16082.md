# Network Configuration Commands

From the command line, you can reconfigure the network in a number of ways. The ifup and ifdown commands can activate and deactivate network devices. The ifconfig command supports detailed changes to individual network devices. The route command supports review of and changes to routing tables.

# ifup/ifdown

You can activate or deactivate the adapter of your choice with the ifup and ifdown commands. For example, either of the following commands will activate the eth0 network adapter. The eth0 device is the standard for the first Ethernet adapter on a system.

```
ifup ifcfg-eth0
ifup eth0
```

As might be expected, you can reverse the process by substituting the ifdown command. Each installed network adapter has a corresponding ifcfg-* file in the /etc/sysconfig/network-scripts directory. When the ifup command is used, it starts the given network adapter based on its configuration file in that directory.

# ifconfig

The ifconfig command is powerful in the area of network configuration. By itself, it lists all currently active network adapters. It can also be used to configure and display network devices. One sample output is shown in Figure 5-11.

The output shown reflects a typical configuration on most systems, with a loopback and a real network adapter, as labeled by their device filenames, lo and eth0 respectively. The loopback adapter supports network tests when a real network connection is not available.

Some systems have a number of network adapters. For example, my home server has two Ethernet cards, a loopback adapter, a virtual bridge to KVM virtual machines, and two virtual bridges to VMware virtual machines. That's six network adapters. But that may not be everything; the ifconfig command lists only active adapters by default. To see the full list, run the ifconfig -a command.

It may help to isolate a specific adapter; for example, the following command isolates settings associated with the first Ethernet adapter:

```
# ifconfig eth0
```