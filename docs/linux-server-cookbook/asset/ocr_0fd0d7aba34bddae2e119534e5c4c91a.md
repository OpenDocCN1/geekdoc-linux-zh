| key_name | mykey |
| name | myfirstvm |
| security_groups | name='allowssh' |
| status | ACTIVE |
| updated | 2022-12-05T18:49:38Z |
| user_id | 6c1f154be7c14eb3b137e73910fad113 |
| volumes_attached | |

Table 16.10: Output fields example creating a server

It is possible to run the Virtual Machines running with the arguments server list as observed in figure 16.20:

```
```bash
[stack@client ~]$ openstack server list -c Name -c Status -c Networks -c Image
+-------+--------+--------------------------+---------+
| Name  | Status | Networks                 | Image   |
+-------+--------+--------------------------+---------+
| myfirstvm | ACTIVE | overlay_network=172.16.0.64 | debian10 |
+-------+--------+--------------------------+---------+```
```

Figure 16.20: Example listing Virtual Machines

Table 16.11 shows the typical tasks performed related to security groups.

| Arguments | Description |
| server delete | Deletes an existing Virtual Machine. |
| server show | Shows all the information about the specified Virtual Machine. |
| server set | Sets different parameters of the Virtual Machine, such as the name or description. |
| server console log show | Shows the log related to the Virtual Machine during the boot process. |
| server stop | Stops the Virtual Machine. |
| server reboot | Reboots the Virtual Machine. |

Table 16.11: Typical tasks related to Virtual Machines

# # Floating IPs

The Virtual Machines attached to an Overlay Network are not accessible from outside of the cluster. To have connectivity to the external world, a Floating IP in the external network should be created and attached to the Virtual Machine. The arguments floating ip create is used to create a new Floating IP to be used