# 25. Creating a RHEL 9 KVM Networked Bridge Interface

By default, the KVM virtualization environment on RHEL 9 creates a virtual network to which virtual machines may connect. It is also possible to configure a direct connection using a MacVTap driver. However, as outlined in the chapter entitled “An Overview of Virtualization Techniques” this approach does not allow the host and guest systems to communicate.

This chapter aims to cover the steps involved in creating a network bridge on RHEL 9, enabling guest systems to share one or more of the host system’s physical network connections while still allowing the guest and host systems to communicate.

In the remainder of this chapter, we will explain how to configure a RHEL 9 network bridge for KVM-based guest operating systems.

# 25.1 Getting the Current Network Manager Settings

A network bridge can be created using the NetworkManager command-line interface tool (nmcli). The NetworkManager is installed and enabled by default on RHEL 9 systems and is responsible for detecting and connecting to network devices and providing an interface for managing networking configurations.

A list of current network connections on the host system can be displayed as follows:

```
# nmcli con show
NAME UUID TYPE DEVICE
eno1 99d40009-6bb1-4182-baad-a103941c90ff ethernet eno1
virbr0 7cb1265e-ffb9-4cb3-aaad-2a6fe5880d38 bridge virbr0
```

The above output shows that the host has an Ethernet network connection established via a device named eno1 and the default bridge interface named virbr0, which provides access to the NAT-based virtual network to which KVM guest systems are connected by default.

Similarly, the following command can be used to identify the devices (both virtual and physical) that are currently configured on the system:

```
# nmcli device show
GENERAL.DEVICE: eno1
GENERAL.TYPE: ethernet
GENERAL.HWADDR: AC:16:2D:11:16:73
GENERAL.MTU: 1500
GENERAL.STATE: 100 (connected)
GENERAL.CONNECTION: eno1
GENERAL.CON-PATH: /org/freedesktop/NetworkManager/
```