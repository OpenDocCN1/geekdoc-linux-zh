Figure 7.27 shows an example using nmtui to define a new bonding combining two interfaces (enp7s0 and enp8s0), thus creating a new virtual bonding interface called bond0:

![](bbox=[0.15, 0.18, 0.85, 0.51])

Running the command ip to list the interfaces will show the physical interfaces and the new bonding interface. The physical interface will show the name of the bonding it belongs to. Refer to figure 7.28:

```
[root@rhel ~]# ip -c -a | tail -10
3: enp7s0: <BROADCAST,MULTICAST,SLAVE,UP,LOWER_UP> mtu 1500 qdisc fq_codel master bond0 state UP group default qlen 1000
    link/ether 52:54:00:10:65:8d brd ff:ff:ff:ff:ff:ff
4: enp8s0: <BROADCAST,MULTICAST,SLAVE,UP,LOWER_UP> mtu 1500 qdisc fq_codel master bond0 state UP group default qlen 1000
    link/ether 52:54:00:10:65:8d brd ff:ff:ff:ff:ff:ff permaddr 52:54:00:c8:55:25
5: bond0: <BROADCAST,MULTICAST,MASTER,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether 52:54:00:10:65:8d brd ff:ff:ff:ff:ff:ff
    inet 10.0.0.218/24 brd 10.0.0.255 scope global dynamic noprefixroute bond0
       valid_lft 3474sec preferred_lft 3474sec
    inet6 fe80::6777:ae7a:a30a:bf68/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
```

Figure 7.28: Output example for the command ip

A file inside of the special directory /proc/net/bonding/, with the name of the bonding interface, is created with the information related to the configuration. The