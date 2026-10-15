
## Table 14.7  SUSE network configuration files in /etc/sysconfig/network

| File | What's set there |
|---|---|
| **ifcfg-interface** | Hostname, IP address, netmask, and more |
| **ifroute-interface** | Interface-specific route definitions |
| **routes** | Default route and static routes for all interfaces |
| **config** | Lots of less commonly used network variables |

With the exceptions of DNS parameters and the system hostname, SUSE sets most networking options in **ifcfg-interface** files in the **/etc/sysconfig/network** directory. One file should be present for each interface on the system.

In addition to specifying the IP address, gateway, and broadcast information for an interface, the **ifcfg-*** files can tune many other network dials. Take a look at the **ifcfg.template** file for a well-commented rundown of the possible parameters. Here's a simple example with our comments:

```
BOOTPROTO='static'      # Static is implied but it doesn't hurt to be verbose.
IPADDR='192.168.1.4/24'  # The /24 defines the NETWORK and NETMASK vars
NAME='AMD PCNet - Fast 79C971' # Used to start and stop the interface.
STARTMODE='auto'       # Start automatically at boot
USERCONTROL='no'       # Disable control through kinternet/kinternet GUI
```

Global static routing information for a SUSE system (including the default route) is stored in the **routes** file. Each line in this file is like a route command with the option names omitted and includes destination, gateway, netmask, interface, and optional extra parameters to be stored in the routing table for use by routing daemons. For the host configured above, which has only a default route, the **routes** file contains the line

```
default 192.168.1.254 - -
```

Routes unique to specific interfaces are kept in **ifroute-interface** files, where the nomenclature of the *interface* component is the same as for the **ifcfg-*** files. The contents have the same format as the **routes** file.

## Red Hat network configuration

Red Hat's network configuration GUI is called **system-config-network**; it's also accessible from the System->Administration menu under the name Network. This tool provides a simple UI for configuring individual network interfaces and static routes. It also has panels for setting up IPsec tunnels, configuring DNS, and adding **/etc/hosts** entries.

Table 14.8 shows the underlying configuration files that this GUI edits.

You set the machine’s hostname in **/etc/sysconfig/network**, which also contains lines that specify the machine’s DNS domain and default gateway.

## Table 14.8  Red Hat network configuration files in /etc/sysconfig

| File | What's set there |
|---|---|
| **network** | Hostname, default route |
| **static-routes** | Static routes |
| **network-scripts/ifcfg-ifname** | Per-interface parameters: IP address, netmask, etc. |

For example, here is a **network** file for a host with a single Ethernet interface:

```
NETWORKING=yes
NETWORKING_IPV6=no
HOSTNAME=redhat.toadranch.com
DOMAINNAME=toadranch.com    ### optional
GATEWAY=192.168.1.254
```

Interface-specific data is stored in **/etc/sysconfig/network-scripts/ifcfg-ifname**, where *ifname* is the name of the network interface. These configuration files set the IP address, netmask, network, and broadcast address for each interface. They also include a line that specifies whether the interface should be configured “up” at boot time.

A generic machine will have files for an Ethernet interface (eth0) and for the loop-back interface (lo). For example,

```
DEVICE=eth0
IPADDR=192.168.1.13
NETMASK=255.255.255.0
NETWORK=192.168.1.0
BROADCAST=192.168.1.255
ONBOOT=yes
```

and

```
DEVICE=lo
IPADDR=127.0.0.1
NETMASK=255.0.0.0
NETWORK=127.0.0.0
BROADCAST=127.255.255.255
ONBOOT=yes
NAME=loopback
```

are the **ifcfg-eth0** and **ifcfg-lo** files for the machine redhat.toadranch.com described in the **network** file above. A DHCP-based setup for eth0 is even simpler:

```
DEVICE=eth0
BOOTPROTO=dhcp
ONBOOT=yes
```

After changing configuration information in **/etc/sysconfig**, run ifdown *ifname* followed by ifup *ifname* for the appropriate interface. If you reconfigure multiple interfaces at once, you can use the command **service network restart** to reset all
