If instead you choose to statically configure IP address information for the eth1 interface, during the OS installation, the corresponding configuration file, ifcfg-eth1, might look like the sample here:

```
TYPE=Ethernet
ONBOOT=yes
BOOTPROTO=none
NAME=eth1
IPADDR=10.72.72.72
PREFIX=24
IPV6ADDR=2002:db8::1/64
```

These fields determine the configuration information for our sample eth1 device. Note how some of the values correspond to parameters used in nmcli invocations. To change the configuration for a device, you can directly modify the appropriate configuration ifcfg-* file or use the nmcli command with the proper options to automatically update or create the file. After making any network configuration changes, you can quickly run the following sequence of commands to take down and bring up the interface:

```
[root@fedora-server ~]# ifdown eth0
[root@fedora-server ~]# ifup eth0
```

To use nmcli to take the interface down and bring it up,

```
[root@fedora-server ~]# nmcli device disconnect eth0
[root@fedora-server ~]# nmcli device connect eth0
```

> TIP Fedora, RHEL, and CentOS로서, the file /usr/share/doc/initscripts/sysconfig.txt explains the options and variables that can be used in the different /etc/sysconfig/network-scripts/ifcfg-* configuration files.

If you need to configure a second network card (for example, eth1), you can use the syntax in the original ifcfg-eth0 by copying and renaming the ifcfg-eth0 file to ifcfg-eth1 and changing the information in the new ifcfg-eth1 file to reflect the second network card's information. When doing this, you have to make sure that the HWADDR variable (media access control, MAC, address) in the new file reflects the MAC address of the actual physical network device you are trying to configure. Once the new ifcfg-eth1 file exists, Fedora will automatically consult the file to configure the device during the next boot or the next time the network service is restarted.

You can also restart the NetworkManager service to make your changes effect, like so:

```
[root@fedora-server ~]# systemctl restart NetworkManager
```