| | |
| --- | --- |
| external | For use on external networks with masquerading enabled, especially for routers. You do not trust the other computers on networks to not harm your computer. Only selected incoming connections are accepted. |
| dmz | For computers in your demilitarized zone that are publicly-accessible with limited access to your internal network. Only selected incoming connections are accepted. |
| work | For use in work areas. You mostly trust the other computers on networks not to harm your computer. Only selected incoming connections are accepted. |
| home | For use in home areas. You mostly trust the other computers on networks not to harm your computer. Only selected incoming connections are accepted. |
| internal | For use on internal networks. You mostly trust the other computers on the networks not to harm your computer. Only selected incoming connections are accepted. |
| trusted | All network connections are accepted. |

*Table 8.1: Predefined zones in firewalld*

It is possible to use the option --get-zones to list the zones available. --get-active-zones lists only the active zones, including the interfaces assigned to those zones. The option --get-default-zone prints the default zone for connections and interface. *Figure 8.4* shows output examples for the options described:

```
```
[root@rhel ~]# firewall-cmd --get-zones
block dmz drop external home internal nm-shared public trusted work
[root@rhel ~]# firewall-cmd --get-active-zones
public
    interfaces: enp1s0 bridge0 bond0 enp7s0 enp8s0 vlan10
[root@rhel ~]# firewall-cmd --get-default-zone
public
```
```

*Figure 8.4: Output example getting zones using command firewall-cmd*

The option --list-all lists information related to the default zone, which is *public* by default, such as the services allowed and the interfaces assigned. It is possible to specify information about another zone, by using the option --zone=name. *Figures 8.5* and *8.6* show both examples: