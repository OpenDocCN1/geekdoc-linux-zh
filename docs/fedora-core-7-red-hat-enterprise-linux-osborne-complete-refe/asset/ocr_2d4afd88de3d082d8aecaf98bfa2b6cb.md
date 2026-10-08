# Interface Configuration Scripts: /etc/sysconfig/network-scripts

The /etc/rc.d/init.d/network file performs the startup operations by executing several specialized scripts located in the /etc/sysconfig/network-scripts directory. The **network** script uses a script in that directory called `ifup` to activate a network connection, and `ifdown` to shut it down; `ifup` and `ifdown` will invoke other scripts tailored to the kind of device being worked on, such as `ifup-ppp` for modems using the PPP protocol, or `ifup-ipv6` for network devices that use IP Protocol version 6 addressing.

> NOTE You can activate and deactivate network interfaces using system-config-network accessible from the System | Administration | Network.

The `ifup` and `ifdown` scripts make use of interface configuration files that bear the names of the network interfaces currently configured, such as `ifcfg-eth0` for the first Ethernet device. These files define shell variables that hold information on the interface, such as whether to start them at boot time. For example, the `ifcfg-eth0` file holds definitions for NETWORK, BROADCAST, and IPADDR, which are assigned the network, broadcast, and IP addresses that the device uses.

The `ifdown` and `ifup` scripts, in turn, hold the `ifconfig` and `route` commands to activate scripts using these variables defined in the interface configuration files. If you want to manually start up an interface with `ifup`, you simply use the interface configuration file as its argument. The following command starts up the second Ethernet card:

```
```
cd /etc/sysconfig/network-scripts
ifup ifcfg-eth1
```
```

Interface configuration files are automatically generated when you configure your network connections, such as with a Red Hat and Fedora’s system-config-network administrative tool. You can also manually edit these interface configuration files, making changes such as whether to start up the interface at boot or not (though using a configuration tool such as system-config-network is easier). A sample `ifcfg-eth0` file is shown here using a static IP address:

```
```
/etc/sysconfig/network-scripts/ifcfg-eth0
DEVICE=eth0
BOOTPROTO=static
BROADCAST=192.168.0.255
IPADDR=192.168.0.1
NETMASK=255.255.255.0
NETWORK=192.168.0.0
ONBOOT=yes
```
```

A DHCP-based interface would look something like this, where BOOTPROTO is assigned dhcp:

```
```
/etc/sysconfig/network-scripts/ifcfg-eth0
DEVICE=eth0
BOOTPROTO=dhcp
HWADDR=00:00:00:00:00:01
TYPE=Ethernet
ONBOOT=yes
```
```