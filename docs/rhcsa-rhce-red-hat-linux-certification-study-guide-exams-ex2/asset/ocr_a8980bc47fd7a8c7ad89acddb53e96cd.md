# FIGURE 3-11

The differences between static and dynamic network configuration

```
[root@Maui ~]# diff ifcfg-eth0 /etc/sysconfig/network-scripts/ifcfg-eth0
1,4c1,17
< DEVICE="eth0"
< HWADDR="F0:DE:F1:06:C6:DC"
< NM_CONTROLLED="yes"
< ONBOOT="no"
---
> DEVICE=eth0
> NM_CONTROLLED=yes
> ONBOOT=no
> BOOTPROTO=none
> NETMASK=255.255.0
> TYPE=Ethernet
> IPV6INIT=no
> USERCTL=no
> HWADDR=f0:de:f1:06:c6:dc
> DEFROUTE=yes
> PEERROUTES=yes
> IPV4_FAILURE_FATAL=yes
> NAME="System eth0"
> UUID=5fb06b0d-0bb0-7ffb-45f1-d6edd5f3e03
> IPADDR=192.168.122.60
> GATEWAY=192.168.122.1
> DNS1=192.168.122.1
[root@Maui ~]#
```

# TABLE 3-6 Network Configuration Directives in the /etc/sysconfig/network-scripts Directory

| Directive | Description |
|---|---|
| DEVICE | Network device; eth0 is the first Ethernet network card |
| HWADDR | Hardware address for the network card |
| NM_CONTROLLED | Binary directive (yes or no) that specifies whether the card is controlled by the NetworkManager service |
| ONBOOT | Binary directive that specifies whether the network device is started during the boot process |
| BOOTPROTO | May be set to none for static configuration, DHCP to acquire IP addresses from a DHCP server |
| NETMASK | Network mask based on a static IP address configuration |
| TYPE | Network type, typically Ethernet |
| IPV6INIT | Binary directive that specifies the use of IPv6 addressing |
| USERCTL | Binary directive for user control of devices |