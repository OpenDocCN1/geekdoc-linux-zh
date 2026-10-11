| --add-port=port/protocol | Allow connections to the port and protocol specified. |
|---|---|
| --add-service=service | Allow connections to the service specified. |
| --add-interface=interface | Assign the interface to the default zone or to the zone specified. |
| --add-source=subnet/mask | Allow connection from the IP or subnet specified. |

Table 8.2: Options to configure zones

It is possible to use `--remove-port`, `--remove-service`, `--remove-interface`, and `--remove-source` to delete configurations from the default zone or the zone specified. To be accepted, the connection, source, and target should be allowed in the zone. Figure 8.7 shows some examples of the usage of the options:

```
[root@rhel ~]# firewall-cmd --add-port=80/tcp
success
[root@rhel ~]# firewall-cmd --add-service=https
success
[root@rhel ~]# firewall-cmd --remove-interface=vlan10
success
[root@rhel ~]# firewall-cmd --add-interface=vlan10 --zone=trusted
success
[root@rhel ~]# firewall-cmd --add-source=10.0.0.0/24 --zone=trusted
success
```

Figures 8.7: Using firewall-cmd to manipulate zones

In figure 8.7, the following operations were performed:

+   • The connection to port 80/tcp was allowed.
+   • The connection to the server https (443/tcp) was allowed.
+   • Interface named vlan10 was removed from the default zone.
+   • Interface named vlan10 was added to the zone trusted.
+   • The network 10.0.0.0/24 was added as an allowed source in the zone trusted.

Changes in firewalld are kept in memory (runtime configuration) till they are converted to permanent rules. The options added as permanent with the option --permanent are not active till the configuration is reloaded with the option --reload. Figure 8.8 shows how a permanent rule is only applied after the configuration is reloaded: