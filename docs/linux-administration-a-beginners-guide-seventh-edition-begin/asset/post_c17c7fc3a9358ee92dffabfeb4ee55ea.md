
# Viewing IPv6 addresses and Connection Information

To display the IPv6 addresses on all interfaces, you can use the ip command like so:

```
[root@server ~]# ip -6 a show
```

To display the IPv6 address associated with the eth0 connection, you can use the nmcli command like so:

```
[root@server ~]# nmcli -f ip6.address connection show eth0
```

# Configuring IPv6 Address and Connection Information

To use the ip command to assign an IPv6 address (for example, 2001:DB8::1) to the interface eth0, you would use this command:

```
[root@server ~]# ip -6 addr add 2001:DB8::1/64 dev eth0
```

To use to delete the IPv6 address created previously, this type:

```
[root@server ~]# ip -6 addr del 2001:DB8::1/64 dev eth0
```

The ifconfig command can also be used to assign an IPv6 address to an interface. For example, we can assign the IPv6 address 2001:DB8::3 to eth2 by running the following:

```
[root@server ~]# ifconfig eth2 inet6 add 2001:DB8::3/64
```

To use nmcli to add a new connection profile named foobar-ipv6 that specifies an IPv6 address for eth1, type

```
[root@server ~]# nmcli connection add con-name foobar-ipv6 \
name eth1 type ethernet6 2001:DB8::1/64
```

Recall that a device can have only one connection active on it at a time. So, to activate the new foobar-ipv6 connection on the eth1 device, you have to run

```
[root@server ~]# nmcli connection up foobar-ipv6
```

Activating a connection profile on a device effectively deactivates the current active connection on the interface device.

# IP Aliasing

IP aliasing is used for assigning multiple IP addresses to a single network interface. In older Linux distros, aliasing is implemented by enumerating instance of the same interface followed by a colon—for example, eth0 is the main interface, eth0:0 is an aliased interface, eth0:1 is also an aliased interface, eth0:2 is another aliased interface, and so on.

Configuring an alias is just like configuring any other interface: Simply use ifconfig or ip utility. For example, to set eth0:0 with the 10.0.0.2 and netmask 255.255.255.0, you would do the:

```
[root@server ~]# ifconfig eth0:0 10.0.0.2 netmask 255.255.255.0
```

To do the same using the ip command, use this:

```
[root@server ~]# ip add 10.0.0.2/24 dev eth0
```

You can view your changes by typing the following:

```
[root@server ~]# ifconfig eth0
eth0: Link:Ethernet HWaddr 00:00:29:AC:55:BD
      inet:10.0.0.2 Bcast:10.0.0.255 Mask:255.255.255.0
      UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
      Interrupt:17 Address:0x140
```

Note that connections made to the aliased interface will communicate on the IP address; however, in most circumstances, any connection originating from the host to another host will use the first assigned IP of the interface. For example, if eth0 is 192.168.1.15 and eth0:0 is 10.0.0.2, a connection from the machine that routed through eth0 will use the IP address 192.168.1.115. The exception to this behavior is for applications that bind to a specific IP address. In those cases, it is possible for the application to originate connections from the aliased IP address. If a host has multiple interfaces, the route table will decide which interface to use. Based on the routing information, the first assigned IP address of the interface will be used.

Confused? Don't worry; it's a little awkward to grasp at. IP is associated with routing as well, so we will revisit this concept later in this chapter.

On Linux distributions that have the latest ip package installed, you no longer have to use the previous interface naming conventions to bind multiple IP addresses to an interface. For a given interface, you now only have to repeat the ip command multiple times with the different IP addresses to achieve the same effect. For example, to bind the IP addresses 10.0.0.2/24 and 192.168.100.100/24 to the eth0 interface, you would run

```
[root@server ~]# ip add 10.0.0.2/24 dev eth0
[root@server ~]# ip add 192.168.100.100/24 dev eth0
```

# Setting Up NICs at Boot Time

The mainstream Linux distributions adopt slightly different approaches when it comes to automating and maintaining network configuration. We will cover the Fedora (and other Red Hat derivatives) specifies in the next section. For other distributions, you need to handle this procedure in one of two ways:

- Use the network administration tool that comes with that to manage the network settings. This is probably the easiest and most reliable method.
- Find the startup script that is responsible for configuring network cards. At the end of the script, add commands is the necessary `ifconfig`, `ip`, or `nmcli` statements. Another place to add commands is in the `rc.local` script or its equivalent—not as pretty, but it works equally well.

# Setting Up NICs Under Fedora, CentOS, and RHEL

Fedora and other Hat-type systems use a simple setup that makes it easy to configure network cards at boot time. It is done through the creation of files in the `/etc/sysconfig/network-scripts` directory. Under their hood, you will find that most network configuration tools create and manage these files for you.

If you're one of those people who like to get directly under the hood, the sections show how to manage the configuration files manually.

For each network interface, there is an `ifcfg` file in `/etc/sysconfig/network-scripts`. This filename is suffixed by the name of the interface. For example, ifcfg-eth0 is for the eth0 device, ifcfg-eth1 is for the eth1 device, and so on.

When doing this, you have to make sure that the HWADDR variable (media access control, MAC, address) in the new file reflects the MAC address of the actual physical network device you are trying to configure. Once the new ifcfg-eth1 file exists, Fedora will automatically consult the file to configure the device during the next boot or the next time the network service is restarted.

You can also restart the NetworkManager service to make your changes effect, like so:

```
[root@fedora-server ~]# systemctl restart NetworkManager
```
