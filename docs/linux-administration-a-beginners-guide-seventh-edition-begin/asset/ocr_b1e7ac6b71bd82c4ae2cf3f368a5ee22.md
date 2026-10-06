# CHAPTER 12 Network Configuration

# Configuring IPv4 Address and Connection Information

To use ifconfig in its simplest form to configure an IP address for an interface, all you need to provide the name of the interface being configured and the IP address. The ifconfig program will deduce the rest of the information from the IP address. Thus, you could enter the following:

```
[root@server]# ifconfig eth1 192.168.1.42
```

This will assign the eth1 device the IP address 192.168.1.42. Because 192.168.1.42 is a class C, the calculated default mask will be 255.255.255.0 and the broadcast address will be 192.168.1.255.

If the IP address you are setting is a class A, B, or C that is subnetted differently, you must set the broadcast and netmask addresses explicitly on the command line, like so:

```
[root@server]# ifconfig dev ip netmask mask broadcast bcast
```

Here, dev is the device you are configuring, ip is the IP address to which you are setting, mask is the netmask, and bcast is the broadcast address.
The following example will assign the eth1 device the IP address 10.1.1.1 with a netmask of 255.255.255.0 and a broadcast of 10.1.1.255.

```
[root@server]# ifconfig eth1 10.1.1.1 netmask 255.255.255.0 broadcast 10.1.1.255
```

To do the same using the ip command, you would type this:

```
[root@server]# ip address 10.1.1.1/24 broadcast 10.1.1.255 dev eth1
```

If you want to automate the detected broadcast address for the interface/network, you can leave out the broadcast option like:

```
[root@server]# ip address 10.1.1.1/24 dev eth1
```

To use ip to update the IP address created previously, use this:

```
[root@server]# ip addr 10.1.1.1/24 broadcast 10.1.1.255 dev eth1
```

To use nmcli to create a new ethernet connection arbitrarily named foobar-ip4 associated with the eth1 device and give it the IP address 10.1.1.1, type:

```
[root@server]# nmcli connection add con-name foobar-ipv4 \ ifname eth1 type ip4 10.1.1.1/24
```

> NOTE On Red Hat-like systems, using nmcli to create a new connection automatically creates a new interface configuration file under the /etc/sysconfig/network-scripts directory. For example, a new Ethernet connection named foobar-connection will have a corresponding configuration file named /etc/sysconfig/network-scripts/ifcfg-foobar-connection.