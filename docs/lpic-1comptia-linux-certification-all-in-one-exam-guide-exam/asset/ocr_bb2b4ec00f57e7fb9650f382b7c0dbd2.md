It's important to remember that this IP address assignment isn't persistent. If you reboot the system, it will be lost. To make it persistent, you need to configure a special file in the /etc/sysconfig/network directory. For example, the file used to configure the first Ethernet interface on some distributions is named ifcfg-eth0.

![](bbox=[0.11, 0.18, 0.97, 0.34])

This file is used to configure the interface when the system is powered on. Sample parameters for this interface are shown here:

```
```
wl:/etc/sysconfig/network # cat ifcfg-eth0
BOOTPROTO='static'
BROADCAST=''
ETHTOOL_OPTIONS=''
IPADDR='192.168.1.81/24'
MU=''
NAME='82545EM Gigabit Ethernet Controller (Copper)'
NETMASK=''
NETWORK=''
REMOTE_IPADDR=''
STARTMODE='auto'
USERCONTROL='no'
LABEL_0=''
IPADDR_0='2607:f0d0:1002:0011:0000:0000:0000:0003'
PREFIXLEN_0='64'
```
```

Some of the configuration options you can use in this configuration file are listed in Table 15-3.

The lines for IPADDR, NETMASK, NETWORK, and BROADCAST are not required if BOOTPROTO set to “dhcp”. The /etc/hostname file configures your Linux system’s hostname.

After making any changes to these files, you will need to restart your network interface to apply the changes. To do this, simply enter ifdown interface followed by ifup interface, where interface is the alias of the interface, such as eth0.

This is all well and good if you want to use a static address assignment, but what if you want to get an address dynamically from a DHCP server? You can configure your network interface to do this using the dhclient command at the shell prompt. The syntax for using this command is dhclient interface. For example, you could enter dhclient eth0 to specify that your eth0 interface get its IP address information dynamically from a DHCP server. This is shown in Figure 15-11.