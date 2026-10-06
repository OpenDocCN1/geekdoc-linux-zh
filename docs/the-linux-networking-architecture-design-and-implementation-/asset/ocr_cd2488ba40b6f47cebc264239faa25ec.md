# 12.3 Configuring a Bridge in Linux 201

![](bbox=[0.167, 0.068, 0.803, 0.303])

FIGURE 12–11
Redundant LAN internetwork.

# 12.3.4 Sample Configuration

The following example shows how you can add a bridge based on the configuration of bridge 1 from the LAN internetwork shown in Figure 12–11:

```
root@tux: # brctl addbr bridge1
root@tux: # brctl addif bridge1 eth0
root@tux: # brctl addif bridge1 eth1
root@tux: # brctl setpathcost bridge1 eth0 5
root@tux: # brctl setpathcost bridge1 eth1 15
root@tux: # ifconfig eth0 0.0.0.0
root@tux: # ifconfig eth1 0.0.0.0
root@tux: # ifconfig bridge1 129.13.42.100 netmask 255.255.255.0 up
```

In this example, we create a bridge, bridge1. Subsequently, we add network adapters. The IP addresses are deleted, because the network adapters are allocated to the LAN internetwork independently-of a protocol.

Nevertheless, it is possible to address the bridge (regardless of a network adapter) by using an IP address. This address is allocated to the virtual adapter, bridge1, as shown in the last command. Each bridge instance has such a virtual network device, which has the same name as its bridge instance.

The outputs of brctl showstp bridge3 and brctl showmacs bridge3 are as:

```
root@tux # brctl showmst bridge 3
bridge3
bridge id               0003.09002744a822b
designated root          0002.09002744da29
root port               path cost               10
max age                 20.00 bridge max age     20.00
hello time              2.00 bridge hello time   2.00
forward delay           15.00 bridge forward delay 15.00
```