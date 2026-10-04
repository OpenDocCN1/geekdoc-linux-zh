# 328 Configuring Networks at Boot Time

Fedora Core comes with another packet sniffer called Ethereal. To find out about Ethereal, visit www.ethereal.com and consult the documentation located in /usr/share/doc/ethereal/ (type is /usr/share/doc/ethereal*) to see the contents of that directory.

# Configuring Networks at Boot Time

You want to start your network automatically every time you boot the system. For that to happen, various startup scripts must contain appropriate commands. You don't have to do anything special other than configure your network (either during installation or by using the Network Configuration tool at a later time). If the network fails at startup, however, you can troubleshoot by checking the files in this section.

To initialize your network, the network-activation script uses a set of files in the /etc/sysconfig directory. For example, the script checks the variables defined in the /etc/sysconfig/network file to decide whether to activate the network. in /etc/sysconfig/network, you see a line with the NETWORKING variable as follows:

```
NETWORKING=yes
```

The network activates only if the NETWORKING variable is set to yes.

A number of scripts in the /etc/sysconfig/network-scripts directory activate specific network interfaces. For example, the configuration file for activating the Ethernet interface eth0 is the file /etc/sysconfig/network-scripts/ifcfg-eth0. Here is what typical /etc/sysconfig/network-scripts/ifcfg-eth0 file contains:

```
DEVICE=eth0
BOOTPROTO=dhcp
ONBOOT=yes
```

The DEVICE line provides the device name. The BOOTPROTO variable is set to dhcp, indicating that the IP address is obtained dynamically by using the Dynamic Host Configuration Protocol (DHCP), a standard method. The ONBOOT variable whether this network interface activates when Fedora Core boots. If your PC has an Ethernet card and you want to activate the eth0 interface at boot time, ONBOOT must be set to yes.

Of course, the configuration file ifcfg-eth0 in the /etc/sysconfig/network-scripts directory works only if your PC has an Ethernet card and the Linux kernel has detected and loaded the specific driver for that.