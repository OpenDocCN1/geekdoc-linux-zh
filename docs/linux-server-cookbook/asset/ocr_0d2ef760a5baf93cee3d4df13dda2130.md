```
[stack@client ~]$ openstack stack output list firststack
+------------------+------------------------------------------------------------+
| output_key       | description                                                |
+------------------+------------------------------------------------------------+
| instance_external_ip | Floating IP address of instance in External network    |
+------------------+------------------------------------------------------------+
[stack@client ~]$ openstack stack output show firststack instance_external_ip
+---------------+----------------------------------------------+
| Field         | Value                                        |
+---------------+----------------------------------------------+
| description   | Floating IP address of instance in External network |
| output_key    | instance_external_ip                         |
| output_value  | 10.0.0.228                                   |
+---------------+----------------------------------------------+
[stack@client ~]$ ssh -i -/.ssh/id_rsa debian@10.0.0.228 lsblk
NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
vda     254:0    0   20G  0 disk
└─vda1  254:1    0   20G  0 part /
vdb     254:16   0    5G  0 disk

```

Figure 16.27: Output value examples for a stack

Table 16.14 shows the typical tasks performed related to Stacks.

| Arguments | Description |
|---|---|
| **stack list** | Lists the existing Stacks. |
| **stack delete** | Deletes an existing Stack, and the resources created |
| **stack show** | Shows all the information about the specified Stack. |
| **stack update** | Updates an existing Stack with a new version of the template. |

Table 16.14: Typical tasks related to Volumes

# Dashboard

The component **Horizon** is responsible for offering a Web dashboard to users for self-service operations. *Figure 16.28* shows an example of the aspect: