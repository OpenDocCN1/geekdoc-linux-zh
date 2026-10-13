
## FIGURE 12-4

Information on the single-file RPM package

```
[michael@server1 ~]$ rpm -qi CorPor
Name        : CorPor                     Relocations: (not relocatable)
Version     : 1.0                        Vendor: (none)
Release     : 1.el6                      Build Date: Wed 16 Feb 2011 09:22:44 AM PST
Install Date: Wed 16 Feb 2011 09:23:04 AM PST   Build Host: server1
Group       : Miscellaneous               Source RPM: CorPor-1.0-1.el6.src.rpm
Size        : 7702360                    License: McGraw-Hill
Signature   : (none)
URL         : http://www.mheducation.com
Summary     : A package with one file
Description :
This is a package with one file, associated with corporate policies.
[michael@server1 ~]$
```

## CERTIFICATION OBJECTIVE 12.04

## Special Network Options

This section relates to three different network options, each associated with an objective for the RHCE exam. The first is related to routing, which requires an understanding of routing tables, the route command, and associated configuration tools and files. The second relates to the configuration of a system as a Kerberos client. It’s not the first time client-side-only configuration has been required on Red Hat exams, as the previous version of the RHCE exam required only the configuration of a system as a Network Information Service (NIS) or a Lightweight Directory Access Protocol (LDAP) client. Just be aware, a Kerberos client does not work unless Network Time Protocol (NTP) clients on both systems are configured to synchronize with the same NTP server.

For the third option, you need to know how to set up an iSCSI client, which can connect to storage over a standard network connection. Just to be clear, as an iSCSI client does not require SCSI hardware, there’s no need to look for that now-older type of server storage media.

## Configure Special IP Routes

As described in the RHCE objectives, you need to know how to “Route IP traffic and create static routes.” That’s really two tasks. First, it’s a standard part of network configuration to set up a default route to an outside network. But there’s also the related task, when a system has two or more network devices, of setting up a special route, using a nondefault device, to a specific network.

## Configure a Default Route

The default route is the path taken by a network message, when the destination address is on an outside network. When a Dynamic Host Configuration Protocol (DHCP) server is working, and is configured to assign gateway addresses, a default route is assigned with the dynamic IP address. That's normally evident in the output to the route -n and netstat -nr commands discussed in Chapter 5. One sample of such output for a system that uses a DHCP server is shown here:

```
Destination Gateway Genmask Flags Metric Ref Use Iface
192.168.122.0 0.0.0.0 255.255.255.0 U 0 0 0 eth0
0.0.0.0 192.168.122.1 0.0.0.0 UG 0 0 0 eth0
```

To review, the default IPv4 address is 0.0.0.0, so the default route goes through the gateway address of 192.168.122.1. In a similar fashion, the default route for a statically configured network system is configured with the GATEWAY directive in its configuration file. Such configuration files are stored in the /etc/sysconfig/network-scripts directory, with names like ifcfg-eth0.

But there are situations, such as a temporary disconnect on a network cable, where the default route is not given by a DHCP server. Perhaps the DHCP server has to be replaced, and you'll have to set up static IP address information. In such cases, the output to the route -n command might look more like the following:

```
Destination Gateway Genmask Flags Metric Ref Use Iface
192.168.122.0 0.0.0.0 255.255.255.0 U 0 0 0 eth0
```

In other words, since the default IP address of 0.0.0.0 is missing, there is no default route. That route can be added temporarily with the route add command. For example, the following command would restore the default route shown earlier:

```
# route add default gw 192.168.122.1
```

If multiple network devices exist on the local system, you can specify it; just for variety, the following command specifies the second Ethernet adapter, eth1:

```
# route add default gw 192.168.122.1 dev eth1
```

To make sure that default route survives a reboot, you'll need to make sure either the system configures that default gateway IP address as part of a static configuration, or the DHCP server used for the network can assign that gateway IP address. To review, Figure 12-5 reflects the way the default gateway IPv4 address is configured with the Network Configuration tool. In addition, you'll need to make sure the added default route survives a reboot, either by a direct change to the ifcfg-ethx configuration file, or indirectly with the Network Configuration tool.

Some systems may have multiple network devices connected to the same network. In that case, you may need to configure a special route. As you might see, special routes are not possible with the console-based Network Configuration tool.

### FIGURE 12-5

A static network configuration with a default gateway

![](img/9139201cfcaf4292284a0eed074928e5_698_0.png)

## Configure a Special Route

One way to configure a special route is with the Network Connections tool. As discussed in Chapter 5, you can start it from a GUI console with the nm-connection-editor command. Select an existing wired or wireless network device, and click Edit. Under either the IPv4 or IPv6 tab, there's a Routes button for special routes. Click it to see the window shown in Figure 12-6.

> The Network Connections tool does not work unless the NetworkManager service in the /etc/init.d directory is active.

![](img/9139201cfcaf4292284a0eed074928e5_698_1.png)

### FIGURE 12-6

A special route for a specific network device

![](img/9139201cfcaf4292284a0eed074928e5_699_0.png)

When applied, it writes a route-eth0 file in the /etc/sysconfig/network-scripts directory. The following is the complete contents of that file:

```
ADDRESS0=192.168.0.0

NETMASK0=255.255.255.0

GATEWAY0=192.168.122.1
```

When the network service is restarted, it's applied to the routing table. Based on the previously configured routing table, the following is the result:

| Destination | Gateway | Genmask | Flags | Metric | Ref | Use | Iface |
|---|---|---|---|---|---|---|---|
| 192.168.0.0 | 192.168.122.1 | 255.255.255.0 | UG | 0 | 0 | 0 | eth0 |
| 192.168.122.0 | 0.0.0.0 | 255.255.255.0 | U | 1 | 0 | 0 | eth0 |
| 0.0.0.0 | 192.168.122.1 | 0.0.0.0 | UG | 0 | 0 | 0 | eth0 |

## Set Up a Kerberos Client

For the purpose of an exam, as well as on the job, it's almost always best to keep the solutions as simple as possible. That's where the Authentication Configuration tool can help. To see what this tool does to help configure a Kerberos client, you could back up the files in the `/etc/sssd` directory, along with the `/etc/nsswitch.conf` configuration file. It's related to the System Security Services Daemon, controlled by the `/etc/init.d/sssd` script. If you've previously configured a system to authenticate via an LDAP server in Chapter 8, the sssd service may already be running.

As there is no RHCE objective related to the configuration of a Kerberos server, that process will not be covered in this book. What you should know is that Kerberos servers as configured on RHEL 6 don't have their own authentication databases. So for a valid client connection to a Kerberos server, you'll also need a connection to a network authentication database such as LDAP.

![](img/9139201cfcaf4292284a0eed074928e5_700_0.png)

*If you configure a Kerberos server, make sure port 88 is open in the relevant firewalls.*

## What Is Kerberos

Kerberos is a network authentication protocol originally developed at the Massachusetts Institute of Technology (MIT) that supports secure identification of networked systems. Since it works with systems, a separate protocol such as LDAP is required for user-based authentication.

Two systems configured with and confirmed by Kerberos can communicate in encrypted format, with a symmetric key. That key is granted by a Key Distribution Center (KDC), which consists of an Authentication Server (AS) and a Ticket Granting Server (TGS). When authentication is confirmed, the Kerberos client gets a ticket good for a limited time, typically eight hours.

Given the importance of time to Kerberos, it may not work unless configured clients and servers also use NTP services, as discussed in Chapters 5 and 17.

## The Graphical Authentication Configuration Tool

One way to open the GUI version of the Authentication Configuration tool is with the `authconfig-gtk` command. That should open the Authentication Configuration tool with the two tabs shown in Figure 12-7. While other authentication databases are supported, the focus is on LDAP, especially since LDAP is the selected network client authentication option for the RHCSA exam. The options in the LDAP half of the Identity And Authentication tab were discussed in Chapter 8.
