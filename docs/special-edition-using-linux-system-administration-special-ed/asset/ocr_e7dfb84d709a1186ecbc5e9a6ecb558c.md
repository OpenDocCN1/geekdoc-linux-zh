There are several key entries in this file related to TCP/IP networks:

+   - **DEVICE:** This entry indicates the device which the file applies to.
+   - **IPADDR:** This entry indicates the primary IP address associated with the interface.
+   - **NETMASK:** This entry indicates the network mask for the interface.
+   - **ONBOOT:** Set to yes or no, this entry indicates if the device should be activated at boot time or not.
+   - **BOOTPROTO:** Indicates the boot protocol, if any, which should be used to configure the network interface’s settings. Possible values are none (network settings are defined manually), dhcp (a DHCP server should be used), and bootp (a BOOTP server should be used).

Once these files are edited, your system’s network settings will be derived from these files at boot time.

# CONFIGURING MULTI-HOMED HOSTS

Up to this point we have been discussing network configuration for hosts with a single network interface. Some consideration needs to be given to hosts with multiple network interfaces, also known as multi-homed hosts.

There are several reasons for a host to have multiple network interfaces, including the following:

+   - The host is acting as a router or gateway between two or more networks.
+   - The host needs to maximize its throughput on the network by using multiple network interfaces to effectively increase the speed with which it can communicate on the network.

Configuring multi-homed hosts is a simple extension of configuring a host with a single network interface:

+   - Each interface has associated with it a kernel module.
+   - Each interface has associated with it a device such as eth0, eth1, or eth2.
+   - For each interface, an appropriate ifconfig command needs to be issued to enable the interface and assign an IP address. You can create a separate interface configuration file such as ifcfg-eth1 or ifcfg-eth2 to automate this process at boot time.
+   - Appropriate routes need to be set, including routes through the correct interface for each network to which the computer is connected.

> **Tip**
> 
> Remember, no matter how many network interfaces a system has and how many networks a system is connected to, a system can only have a single default gateway through a single network interface.