```
[root@rhel ~]# nmcli connection add type bridge ifname bridge0 con-name bridge0
Connection 'bridge0' (8c583fd0-9e9f-471f-9bd1-6884baa40cd9) successfully added.
[root@rhel ~]# nmcli con add type bridge-slave ifname enp7s0 master bridge0
Connection 'bridge-slave-enp7s0' (4e40de6e-4953-4037-af3-90170f54caea) successfully added.
[root@rhel ~]# nmcli con up bridge-slave-enp7s0
Connection successfully activated (D-Bus active path: /org/freedesktop/NetworkManager/ActiveConnection/6)
[root@rhel ~]# nmcli con up bridge0
Connection successfully activated (D-Bus active path: /org/freedesktop/NetworkManager/ActiveConnection/7)
```

Figure 7.31: Output example for the command nmcli

Using **netplan**, it is possible to create a Linux bridge, as shown in the following code as an example:

```
network:
    version: 2
    renderer: networkd
    ethernets:
        enp7s0:
            dhcp4: no
    bridges:
        bridge0:
            dhcp4: yes
            interfaces:
                - enp7s0
```

**Open vSwitch (OVS)** is an open-source project to operate with virtual switches. Nowadays, it is recommended to use OVS instead of *Linux bridges* due to the flexibility, efficiency, and compatibility with more tunnel protocols (*VXLAN*, *GRE*, *and so on*). It is also possible to integrate with *Software Defined Network* solutions. [Figure 7.32](#) shows the communication between two hosts using OVS and acting as a network bridge for Virtual Machines: