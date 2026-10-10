![](bbox=[0.14, 0.07, 0.31, 0.16])

Since firewall rules can quickly become complex, some Linux distributions, such as Fedora 20, implement a **firewall daemon** (firewalld) that can configure iptables with more flexibility through the use of network zones and service names. A **network zone** defines the level of trust for network connections and can be mutable (modification to its definition is allowed) or immutable (its definition cannot be changed). Table 14-3 lists common network zones used by firewalld.

The default zone used on your system is defined in /etc/firewalld/firewalld.conf, and custom zone configuration is stored in /etc/firewalld/zones. You can manage zones and firewall rules that allow or deny traffic by service or port through the use of the **firewall-cmd command**. Some common options to the firewall-cmd command are listed in Table 14-4.

To define a firewall exception for postgresql in your default (current) zone and also ensure that this exception is loaded at boot time, you could use the following commands:

```
[root@server1 ~]# firewall-cmd --add-service=postgresql
success
[root@server1 ~]# firewall-cmd --permanent --add-service=postgresql
success
[root@server1 ~]#
```

You can instead define a firewall exception for traffic by port number. For example, to define a firewall exception for SSH (TCP port 22) in your default (current) zone and also ensure that this exception is loaded at boot time, you could use the following commands:

```
[root@server1 ~]# firewall-cmd --add-port=22/tcp
success
```

| Network Zone | Type | Description |
| :------------ | :----- | :---------------------------------------------------- |
| drop         | Immutable | Deny all incoming connections; outgoing ones are accepted. |
| block        | Immutable | Deny all incoming connections, with ICMP host-prohibited messages issued to the sender. |
| trusted      | Immutable | Allow all network connections. |
| public       | Mutable | Public areas, do not trust other computers. |
| external     | Mutable | For computers with masquerading enabled, protecting a local network. |
| dmz          | Mutable | For computers publicly accessible with restricted access. |
| work         | Mutable | For trusted work areas. |
| home         | Mutable | For trusted home network connections. |
| internal     | Mutable | For internal network, restrict incoming connections. |

Table 14-3 Common network zones