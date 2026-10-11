To test IP addresses, try to ping from another machine on same network on both addresses.

```
```
[root@netmon tmp]# ping -c 4 172.16.1.100
[root@netmon tmp]# ping -c 4 172.16.1.200
[root@netmon tmp]# ifup eth0:0
[root@netmon tmp]# ifdown eth0:0
```
```

It is always a good practice to make a backup copy of ifcfg-eth0 file:

```
```
[root@netmon tmp]#
[root@netmon tmp]# cd /etc/sysconfig/network-scripts/
[root@netmon network-scripts]# ls ifcfg-eth0
[root@netmon network-scripts]# cp ifcfg-eth0 backup.ifcfg-eth0
```
```

Edit your ifcfg-eth0 file to have no IP information and also to be deactivated on boot time.

```
```
DEVICE=eth0
ONBOOT=no
```
```

Shut down eth0 interface:

```
```
[root@netmon network-scripts]# ifdown eth0
[root@netmon network-scripts]#
```
```

Activate network interface:

```
```
[root@netmon network-scripts]# service network restart
```
```

It refers the ifcfg-eth0 configuration file every time you start network service.

# ## Configuring Routing

To view current routing table

The netstat -nr command will provide the contents of the routing table.

```
```
[root@netmon tmp]# netstat -nr
```
```

OR

```
```
[root@netmon tmp]# route -n
```
```

# ## Changing Your Default Gateway

Your PC needs to have a single default gateway. DHCP servers automatically assign a default gateway to DHCP-configured NICs, but NICs with configured, static IP addresses will need to have a manually configured default gateway. This can be done with a simple command.

```
```
[root@netmon tmp]# route add default gw 172.16.1.1 eth0
```
```