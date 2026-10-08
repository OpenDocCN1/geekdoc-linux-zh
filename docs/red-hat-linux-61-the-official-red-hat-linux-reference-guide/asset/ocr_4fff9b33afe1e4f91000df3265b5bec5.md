# Interface Configuration Files

Interface configuration files control the software interfaces for individual network devices. As the system boots, it uses these files to determine what interfaces to bring up and how to configure them. These files are usually named ifcfg-<name>, where <name> refers to the name of the device that the configuration file controls.

# 8.2.1. Ethernet Interfaces

One of the most common files is ifcfg-eth0, which controls the first Ethernet interface card or NIC in the system. In a system with multiple NICs, there are multiple ifcfg-eth-<X> files (where <X> is a unique number corresponding to a specific interface). Because each device has its own configuration file, an administrator can control how each interface functions individually. Below is a sample ifcfg-eth0 file for a system using IP address:

```
DEVICE=eth0
BOOTPROTO=none
ONBOOT=yes
NETWORK=10.0.0.1
NETMASK=255.255.255.0
IPADDR=10.0.1.27
USERCTL=no
```

The values required in a configuration file can change based on other values. For example, the ifcfg-eth0 file for an interface using DHCP looks a bit different, because IP information is provided by the DHCP server:

```
DEVICE=eth0
BOOTPROTO=dhcp
ONBOOT=yes
```

The Network Administration Tool (redhat-config-network) is an easy way to make changes to the various network interface configuration files (see the chapter titled Network Configuration in the Red Hat Linux Customization Guide for detailed instructions on using this tool).

However, it is also possible to edit the configuration files for a given network interface by hand. Below is a list of the configurable parameters in an Ethernet configuration file:

+   - BOPROTO=<protocol>, where <protocol> is one of the following:
  - none No Boot-time protocol should be used.
  - bootp — The BOOTP protocol should be used.
  - dhcp — The DHCP protocol should be used.
- BROADCAST=<address>, where <address> is the broadcast address. This directive is deprecated.
- DEVICE=<name>, where <name> is the name of the physical device (except for dynamically-allocated PPP devices where it is the logical name).
- DNS{1,2}=<address>, where address is a server address to be placed in /etc/resolv.conf if PEERDNS is set to yes.
- IPADDR=<address>, where <address> is the IP address.
- NETMASK=<mask>, where <mask> is the netmask value.