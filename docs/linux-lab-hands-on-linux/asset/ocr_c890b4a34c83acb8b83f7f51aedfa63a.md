# Set NIC’s Speed Configuration with ethtool

Unlike mii-tool, ethtool settings can be permanently set as a part of the interface configuration script with the ETHTOOL_OPTS variable. In our next example, the settings will be set to 100Mbps, full duplex with no chance for autonegotiation on the next reboot:

```
#
# File: /etc/sysconfig/network-script/ifcfg-eth0
#
DEVICE=eth0
IPADDR=192.168.1.100
NETMASK=255.255.0.0
BOOTPROTO=static
ONBOOT=yes
ETHTOOL_OPTS="speed 100 duplex full autoneg off"
```

The ethtool settings can also be changed from the command line by using the -s switch followed by the interface name and its desired configuration parameters, as shown follows:

```
[root@netmon tmp]# ethtool -s eth1 speed 100 duplex full autoneg off
```

# Hostname Configuration

# Configuring the /etc/hosts File

The /etc/hosts file is just a list of IP addresses and their corresponding server names. Your server will typically check this file before referencing DNS. If the name is found with a corresponding IP address, DNS will not be queried at all. Add a quick /etc/hosts file entry:

```
172.16.1.100 netx
```

You can check the network connectivity by using ping command:

```
[root@netmon tmp]# ping netx
PING zero (172.16.1.100) 56(84) bytes of data.
64 bytes from netx (172.16.1.100): icmp_seq=0 ttl=64 time=0.185 ms
64 bytes from netx (172.16.1.100): icmp_seq=1 ttl=64 time=0.064 ms
-----
```

# The loopback Interface’s localhost Entry

Usually, the first entry in /etc/hosts defines the IP address of the server’s virtual loopback interface. This is usually mapped to the name localhost.localdomain (the universal name used when a server refers to itself) and localhost (the shortened alias name). By default, Fedora inserts the hostname of the server between the 127.0.0.1 and the localhost entries like this:

```
127.0.0.1 netmon localhost.localdomain localhost
```

When the server is connected to the Internet, this first entry after the 127.0.0.1 needs to be the fully qualified domain name (FQDN) of the server—for example, netmon.mysite.com:

```
127.0.0.1 netmon.spit.ac.in localhost.localdomain localhost
```